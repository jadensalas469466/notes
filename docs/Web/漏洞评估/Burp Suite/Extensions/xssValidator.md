一款用于自动化验证 XSS 漏洞的 Burp Suite 工具。

# 1 部署

安装 [phantomjs](https://phantomjs.org/) 用于接收攻击反馈

编写脚本 D:\software\phantomjs\bin\xss.js

```js
/**
 * This is a basic phantomJS script that will be used together
 * with the xssValidator burp extender.
 *
 * This script launches a web server that listens by default 
 * on 127.0.0.1:8093. The server listens for POST requests with 
 * http-response data.
 *
 * http-response should contain base64 encoded HTTP response as
 * passed from burp intruder. The server will decode this data, 
 * and build a WebPage bassed of the markup provided.
 *
 * The WebPage will be injected with the js-overrides.js file, 
 * which contains triggers for suspicious JS functions, such as
 * alert, confirm, etc. The page will be evaluated, and the DOM
 * triggers will alert us of any suspicious JS.
*/
var DEBUG = true

var system = require('system');
var fs = require('fs');

// Create xss object that will be used to track XSS information
var xss = new Object();
xss.value = 0;
xss.msg = "";

// Create webserver object
var webserver = require('webserver');
server = webserver.create();

// Server config details
var host = '127.0.0.1';
var port = '8093';

/**
 * parse incoming HTTP responses that are provided via BURP intruder.
 * data is base64 encoded to prevent issues passing via HTTP.
 */
parsePage = function(data,url,headers) {
	if (DEBUG) {	
		console.log("Beginning to parse page");
		console.log("\tURL: " + url);
		console.log("\tHeaders: " + headers);
	}

	var html_response = "";
	var headerArray = { };

	// Parse headers and add to customHeaders hash
	var headerLines = headers.split("\n");

	// Remove several unnecessary lines including Request, and double line breaks
	headerLines.splice(0,1);
	headerLines.pop();
	headerLines.pop();

	for (var i = 0; i < headerLines.length; i++) {
		// Split by colon now
		var lineItems = headerLines[i].split(": ");

		headerArray[lineItems[0]] = lineItems[1].trim();
	}

	wp.customHeaders = headerArray;

	wp.setContent(data, decodeURIComponent(url));

	// Evaluate page, rendering javascript
	xssInfo = wp.evaluate(function (wp) {				
                var tags = ["a", "abbr", "acronym", "address", "applet", "area", "article", "aside", "audio", "audioscope", "b", "base", "basefont", "bdi", "bdo", "bgsound", "big", "blackface", "blink", "blockquote", "body", "bq", "br", "button", "canvas", "caption", "center", "cite", "code", "col", "colgroup", "command", "comment", "datalist", "dd", "del", "details", "dfn", "dir", "div", "dl", "dt", "em", "embed", "fieldset", "figcaption", "figure", "fn", "font", "footer", "form", "frame", "frameset", "h1", "h2", "h3", "h4", "h5", "h6", "head", "header", "hgroup", "hr", "html", "i", "iframe", "ilayer", "img", "input", "ins", "isindex", "kbd", "keygen", "label", "layer", "legend", "li", "limittext", "link", "listing", "map", "mark", "marquee", "menu", "meta", "meter", "multicol", "nav", "nobr", "noembed", "noframes", "noscript", "nosmartquotes", "object", "ol", "optgroup", "option", "output", "p", "param", "plaintext", "pre", "progress", "q", "rp", "rt", "ruby", "s", "samp", "script", "section", "select", "server", "shadow", "sidebar", "small", "source", "spacer", "span", "strike", "strong", "style", "sub", "sup", "table", "tbody", "td", "textarea", "tfoot", "th", "thead", "time", "title", "tr", "tt", "u", "ul", "var", "video", "wbr", "xml", "xmp"];
                var eventHandler = ["mousemove","mouseout","mouseover"]

                // Search document for interactive HTML elements, and hover over each
                // In attempt to trigger event handlers.
                tags.forEach(function(tag) {
                        currentTags = document.querySelector(tag);
                        if (currentTags !== null){
                                eventHandler.forEach(function(currentEvent){
		                        var ev = document.createEvent("MouseEvents");
                                        ev.initEvent(currentEvent, true, true);
                                        currentTags.dispatchEvent(ev);
                                });
                        }
                });
		// Return information from page, if necessary
		return document;
	}, wp);
	if(xss) {
		// xss detected, return
		return xss;
	}
	return false;
};

/**
 * After retriving data it is important to reinitialize certain
 * variables, specifically those related to the WebPage objects.
 * Without reinitializing the WebPage object may contain old data,
 * and as such, trigger false-positive messages.
 */
reInitializeWebPage = function() {
	wp = require("webpage").create();
	xss = new Object();
	xss.value = 0;
	xss.msg = "";

	// web page settings necessary to adequately detect XSS
	wp.settings = {
		loadImages: true,
		localToRemoteUrlAccessEnabled: true,
		javascriptEnabled: true,
		webSecurityEnabled: false,
		XSSAuditingEnabled: false,
	};

	// Custom handler for alert functionality
	wp.onAlert = function(msg) {
		console.log("On alert: " + msg);
		
		xss.value = 1;
		xss.msg += 'XSS found: alert(' + msg + ')';
	};
	wp.onConsoleMessage = function(msg) {
		console.log("On console.log: " + msg);
		
		xss.value = 1;
		xss.msg += 'XSS found: console.log(' + msg + ')';
	};
	wp.onConfirm = function(msg) {
		console.log("On confirm: " + msg);
		
		xss.value = 1;
		xss.msg += 'XSS found: confirm(' + msg + ')';
	};

	wp.onPrompt = function(msg) {
		console.log("On prompt: " + msg);
		
		xss.value = 1;
		xss.msg += 'XSS found: prompt(' + msg + ')';
	};
	
	wp.onError = function(msg) {
		console.log("Parse error: "+msg);
		xss.value = 2;
		xss.msg +='Probable XSS found: execution-error: '+msg;
	};
	return wp;
};

// Initialize webpage to ensure that all variables are
// initialized.
var wp = reInitializeWebPage();

// Start web server and listen for requests
var service = server.listen(host + ":" + port, function(request, response) {
	
	if(DEBUG) {
		console.log("\nReceived request with method type: " + request.method);
	}

	// At this point in time we're only concerned with POST requests
	// As such, only process those.
	if(request.method == "POST") {
		// Grab pageResponse from POST Data and base64 decode.
		// pass result to parsePage function to search for XSS.
		var pageResponse = request.post['http-response'];
		var pageUrl = request.post['http-url'];
		var responseHeaders = request.post['http-headers'];

		pageResponse = atob(pageResponse);
		pageUrl = atob(pageUrl);
		responseHeaders = atob(responseHeaders);

		//headers = JSON.parse(responseHeaders);
		headers = responseHeaders;

		if(DEBUG) {
			console.log("Processing Post Request");
		}

		xssResults = parsePage(pageResponse,pageUrl,headers);

		// Return XSS Results
		if(xssResults) {
			// XSS is found, return information here
			response.statusCode = 200;
			response.write(JSON.stringify(xssResults));
			response.close();
		} else {
			response.statusCode = 201;
			response.write("No XSS found in response");
			response.close();
		}
	} else {
		response.statusCode = 500;
		response.write("Server is only designed to handle POST requests");
		response.close();
	}

	// Re-initialize webpage after parsing request
	wp = reInitializeWebPage();
	pageResponse = null;
	xssResults = null;
});
	

```

编写 D:\software\phantomjs\bin\phantomjs.bat 脚本

```bat
@echo off
.\phantomjs.exe .\xss.js
```

> 确保此脚本与 phantomjs.exe 和 xss.js 在同一目录下
>
> 可在桌面创建快捷方式

刷新插件列表

![刷新插件列表](./../../../../../images/xssValidator/%E5%88%B7%E6%96%B0%E6%8F%92%E4%BB%B6%E5%88%97%E8%A1%A8.png)

搜索 xss 的相关插件

![搜索 xss 的相关插件](./../../../../../images/xssValidator/%E6%90%9C%E7%B4%A2%20xss%20%E7%9A%84%E7%9B%B8%E5%85%B3%E6%8F%92%E4%BB%B6.png)

选择 xssValidator 插件进行安装

![选择 xssValidator 插件进行安装](./../../../../../images/xssValidator/%E9%80%89%E6%8B%A9%20xssValidator%20%E6%8F%92%E4%BB%B6%E8%BF%9B%E8%A1%8C%E5%AE%89%E8%A3%85.png)

# 2 使用

在已安装中加载 XSS Validator 插件

![在已安装中加载插件](./../../../../../images/xssValidator/%E5%9C%A8%E5%B7%B2%E5%AE%89%E8%A3%85%E4%B8%AD%E5%8A%A0%E8%BD%BD%E6%8F%92%E4%BB%B6.png)

加载以后会出现 xssValidator

![加载以后会出现 xssValidator](./../../../../../images/xssValidator/%E5%8A%A0%E8%BD%BD%E4%BB%A5%E5%90%8E%E4%BC%9A%E5%87%BA%E7%8E%B0%20xssValidator.png)

可以在 payloads 中加入自己的 payload

![可以在 payloads 中加入自己的 payload](./../../../../../images/xssValidator/%E5%8F%AF%E4%BB%A5%E5%9C%A8%20payloads%20%E4%B8%AD%E5%8A%A0%E5%85%A5%E8%87%AA%E5%B7%B1%E7%9A%84%20payload.png)

> 注意格式要与插件中的相同，js 代码要换成 JAVASCRIPT
>
> 插件不用时记得关闭

访问 XSS (Reflected)

> http://a-centos7-6.local/dvwa/vulnerabilities/xss_r/

运行 phantomjs.bat

burp 开启拦截

提交测试

![提交测试](./../../../../../images/xssValidator/%E6%8F%90%E4%BA%A4%E6%B5%8B%E8%AF%95.png)

发送到 Intruder ，添加 payload 位置

payload 类型选择 Extension-generated

![payload 类型选择 Extension-generated](./../../../../../images/xssValidator/payload%20%E7%B1%BB%E5%9E%8B%E9%80%89%E6%8B%A9%20Extension-generated.png)

选择对应的生成器

![选择对应的生成器](./../../../../../images/xssValidator/%E9%80%89%E6%8B%A9%E5%AF%B9%E5%BA%94%E7%9A%84%E7%94%9F%E6%88%90%E5%99%A8.png)

在资源池中配置单线程

![在资源池中配置单线程](./../../../../../images/xssValidator/%E5%9C%A8%E8%B5%84%E6%BA%90%E6%B1%A0%E4%B8%AD%E9%85%8D%E7%BD%AE%E5%8D%95%E7%BA%BF%E7%A8%8B.png)

> 多线程对性能要求较高

在 xssValidator 中查看 Grep Phrase

![在 xssValidator 中查看 Grep Phrase](./../../../../../images/xssValidator/%E5%9C%A8%20xssValidator%20%E4%B8%AD%E6%9F%A5%E7%9C%8B%20Grep%20Phrase.png)

>```
>fy7sdufsuidfhuisdf
>```
>
>这段字符会显示在成功的响应包中

清空 检索-匹配 添加 Grep Phrase

![清空 检索-匹配 添加 Grep Phrase](./../../../../../images/xssValidator/%E6%B8%85%E7%A9%BA%20%E6%A3%80%E7%B4%A2-%E5%8C%B9%E9%85%8D%20%E6%B7%BB%E5%8A%A0%20Grep%20Phrase.png)

> 这样会在成功的响应中标记

开始攻击，查看结果

> 注意，在存储类型的漏洞使用自动攻击可能导致目标浏览器崩溃

![开始攻击，查看结果](./../../../../../images/xssValidator/%E5%BC%80%E5%A7%8B%E6%94%BB%E5%87%BB%EF%BC%8C%E6%9F%A5%E7%9C%8B%E7%BB%93%E6%9E%9C.png)

>可以在 P grep 中看到成功的结果，每次成功都会添加字符串
>
>```html
><script>alert(299792458)</script>
>```

> 即
>
> ```
> fy7sdufsuidfhuisdf
> ```

在 P grep 排序，选中成功的内容，右击可以查看成功的数量

![在 P grep 排序，选中成功的内容，右击可以查看成功的数量](./../../../../../images/xssValidator/%E5%9C%A8%20P%20grep%20%E6%8E%92%E5%BA%8F%EF%BC%8C%E9%80%89%E4%B8%AD%E6%88%90%E5%8A%9F%E7%9A%84%E5%86%85%E5%AE%B9%EF%BC%8C%E5%8F%B3%E5%87%BB%E5%8F%AF%E4%BB%A5%E6%9F%A5%E7%9C%8B%E6%88%90%E5%8A%9F%E7%9A%84%E6%95%B0%E9%87%8F.png)

> 使用完记得关闭插件

---

参考链接

- [xssValidator](https://github.com/portswigger/xss-validator)