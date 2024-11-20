一种服务器端脚本语言。

## 1 部署

```shell
┌──(root㉿kali)-[~]
└─# apt install -y php php-gd php-mysql libapache2-mod-php
```

## 2 初始化

编辑配置文件

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/php/8.2/apache2/php.ini
```

禁用敏感函数

```
323 disable_functions = exec,system
```

设置时区

```
979 date.timezone = PRC
```

重启 apache 生效

```shell
┌──(root㉿kali)-[~]
└─# systemctl restart apache2
```

### 2.1 禁用敏感函数

> 禁用的敏感函数会出现在 phpinfo 的 `disable_functions` 中
> 
>  [LAMP.md](..\..\LAMP\LAMP.md) 

浏览器访问 phpinfo ，查找 `disable_functions`

| Core |
|:----:|

| Directive         | Local Value | Master Value |
| ----------------- | ----------- | ------------ |
| disable_functions | exec,system | exec,system  |

> 发现 `phpinfo` 中显示 `exec`  和 `system` 已经被禁用

## 3 使用

### 3.1 PHP 读写Cookie

> JSP ASP ASPX PYTHON GO 也可以
> 
> 实验前要先禁止浏览器自动删除 Cookie

### 3.1.1 创建 Cookie

在 PHP 中通过 setcookie()函数创建 Cookie

```
bool setcookie ( string $name [, string $value [, int $expire = 0 [, string $path [, string$domain [, bool $secure = false [, bool $httponly = false ]]]]]])
```

| 操作       | 描述                                                                                                                                                                                 | 必填  | 举例                                                                                                                               |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- | -------------------------------------------------------------------------------------------------------------------------------- |
| name     | cookie 的名字                                                                                                                                                                         | 是   | 使用 $_COOKIE['cookiename'] 调用名为  cookiename 的 cookie。                                                                             |
| value    | cookie 的值，存放在客户端，不要存放敏感数据                                                                                                                                                          | 是   | 假定 name 是 ’cookiename’ ，可以通过 $_COOKIE[‘cookiename’] 取得其值。                                                                        |
| expire   | Cookie 过期的时间。这是个 Unix 时间戳，即从 Unix 纪元开始的秒数。换而言之，通常用 time() 函数再加上秒数来设定 cookie  的失效期。或者用 mktime()来实现                                                                                  | 否   | time()+86400*30 将设定cookie 30 天后失效。如果未设定，cookie 将会在会话结束后（一般是浏览器关闭）失效。                                                             |
| path     | Cookie 在服务器端的有效路径                                                                                                                                                                  | 否   | 如果该参数设为 ‘/‘ 的话， cookie 就在整个 domain 内有效，如果设为 ‘/foo/‘， cookie 就只在 domain 下的 /foo/ 目录及其子目录内有效，例如 /foo/bar/。默认值为设定 cookie 的当前目录。     |
| domain   | 该 Cookie 有效的域名                                                                                                                                                                     | 否   | 要使 cookie 能在如 example.com 域名下的所有子域都有效的话，该参数应该设为 ‘.example.com’。虽然并不是必须的，但加上它会兼容更多的浏览器。如果该参数设为 www.example.com  的话，就只在 www 子域内有效。 |
| secure   | 指明 Cookie 是否仅通过安全的 HTTPS 连接传送。当设成 TRUE 时，cookie 仅在安全的连接中被设置。默认值为 FALSE                                                                                                             | 否   | 0 或 1                                                                                                                            |
| httponly | 设为 true 后，只能通过 http 访问，javascript 无法访问;防止 xss 读取 cookie;php5.2 以上版本已支持 HttpOnly 参数的设置，同样也支持全局的 HttpOnly 的设置，在 php.ini 中， session.cookie_httponly=ture  来开启全局的 Cookie 的 HttpOnly 属性 | 否   | setcookie(“abc”, “test”,NULL, NULL, NULL, NULL, TRUE)                                                                            |

**创建名称为 name 的 cookie，值为 root**

切换到站点根目录

```
[root@CentOS-76 ~]# cd /var/www/html/
```

创建文件 cookie1.php

```
[root@CentOS-76 html]# vim cookie1.php
```

```php
<?php
setcookie('name','root');
setcookie('hello','666',time()+3600);
echo date('Y-m-d H:i:s');
?>
```

| 操作                                    | 描述                                        |
| ------------------------------------- | ----------------------------------------- |
| setcookie('name','root');             | 设置名称为 name 的 cookie，值为 root               |
| setcookie('hello','666',time()+3600); | 设置名称为 hello 的 cookie 的值为 666，有效时间为 3600 秒 |
| echo date('Y-m-d H:i:s');             | 输出当前时间                                    |

浏览器访问

> http://192.168.6.76/cookie1.php

按 F12 查看 Cookie 信息

![](/img/PHP/按 F12 查看 Cookie 信息.png)

> 从图中可以看到 domain 没有设置默认为 当前站点域名，path 默认为 / ，也就是这个 Cookie 在整个站点内是有效的，第一个 cookie 没有设置过期时间 expire，默认为 Session ，说明当浏览器关掉后，会失效。第二个 cookie 过期时间为访问页面时开始 1 个小时候失效。

### 3.1.2 读取 Cookie

**读取名称为 name 的 cookie 的值**

创建文件 cookie2.php

```
[root@CentOS-76 html]# vim cookie2.php
```

```php
<?php
echo $_COOKIE['name'];
echo "<br/>";
echo $_COOKIE['hello'];
?>
```

| 操作                      | 描述                                |
| ----------------------- | --------------------------------- |
| echo $_COOKIE['name'];  | 读取名称为 name 的 cookie 的值并输出到当前页面    |
| echo "\<br/>";          | 输出换行，为了显示更明显些，将两个 cookie 的值用换行符间隔 |
| echo $_COOKIE['hello']; | 读取名称为 hello 的 cookie 的值并输出到当前页面   |

浏览器访问

> http://192.168.6.76/cookie2.php

可看到有两个值

![](/img/PHP/可看到有两个值.png)

关闭浏览器，重新访问

![](/img/PHP/关闭浏览器，重新访问.png)

> 可以看到只有一个值
> 
> 原因是在 cookie1.php 中没有设置过期时间，关闭浏览器后会失效。而 cookie2.php 设置的过期时间为 1 个小时。

### 3.1.3 删除 Cookie

### 3.1.4 setcookie()函数删除

编辑文件 delcookie.php

```
[root@CentOS-76 html]# vim delcookie.php
```

```php
<?php
setcookie('hello',null,time()-1);
?>
```

| 操作                                 | 描述                   |
| ---------------------------------- | -------------------- |
| setcookie('xuegod',null,time()-1); | 删除名称为 hello 的 cookie |

浏览器先后访问两个文件

> http://192.168.6.76/cookie1.php
> 
> http://192.168.6.76/cookie2.php

![](/img/PHP/浏览器先后访问两个文件.png)

> 可以看到两个值都在

浏览器访问

> http://192.168.6.76/delcookie.php

刷新 `cookie2.php`

![](/img/PHP/刷新 cookie2.php.png)

> 发现 `666` 已被删除

### 3.1.5 浏览器手动删除

浏览器先后访问两个文件

> http://192.168.6.76/cookie1.php
> 
> http://192.168.6.76/cookie2.php

按 F12 选择删除即可

![](/img/PHP/按 F12 选择删除即可.png)

再次刷新 `cookie2.php`

![](/img/PHP/再次刷新 cookie2.php.png)

> 发现已经删除。

### 3.2 PHP 调用并执行 Linux 命令

| PHP 敏感函数 |
|:--------:|

| 操作           | 描述                                          |
| ------------ | ------------------------------------------- |
| exec()       | 允许执行一个外部程序（如 UNIX Shell 或 CMD 命令等）          |
| system()     | 允许执行一个外部程序并回显输出，类似于 passthru()              |
| passthru()   | 允许执行一个外部程序并回显输出，类似于 exec()                  |
| popen()      | 可通过 popen() 的参数传递一条命令，并对 popen() 所打开的文件进行执行 |
| proc_open()  | 执行一个命令并打开文件指针用于读取以及写入                       |
| shell_exec() | 通过 Shell 执行命令，并将执行结果作为字符串返回                 |

> 这些函数对于 linux 服务器是及其不安全，如果被执行时一件很危险的事情。所以一般服务器都会禁用这些函数。

### 3.2.1 exec()

新建文件 exec.php

```
[root@CentOS-76 html]# vim exec.php
```

```php
<?php
$test = "id";
exec($test,$array);
print_r($array);
?>
```

| 操作                  | 描述                                 |
| ------------------- | ---------------------------------- |
| $test = "id";       | id 是 linux 下的用于显示用户的 ID，以及所属群组的 ID |
| exec($test,$array); | 执行命令                               |
| print_r($array);    | 打印                                 |

浏览器访问

> http://192.168.6.76/exec.php

输出

```
Array ( [0] => uid=48(apache) gid=48(apache) groups=48(apache) ) 
```

### 3.2.1.1 扩展

编辑文件 exec.php

```
[root@CentOS-76 html]# vim exec.php
```

```php
<?php
$test = $_GET['hello'];
exec($test,$array);
print_r($array);
?>
```

浏览器访问

> http://192.168.6.76/exec.php

地址栏访问

> http://192.168.6.76/exec.php?hello=id

输出

```
uid=48(apache) gid=48(apache) groups=48(apache) 
```

### 3.1.6 system()

新建文件 system.php

```
[root@CentOS-76 html]# vim system.php
```

```php
<?php
$test = "id";
$last = system($test);
?>
```

浏览器访问

> http://192.168.6.76/system.php

输出

```
uid=48(apache) gid=48(apache) groups=48(apache) 
```

### 3.1.7 passthru()

新建文件 passthru.php

```
[root@CentOS-76 html]# vim passthru.php
```

```php
<?php
$test = "id";
passthru($test);
?>
```

浏览器访问

> http://192.168.6.76/passthru.php

输出

```
uid=48(apache) gid=48(apache) groups=48(apache)
```

### 3.1.8 popen()

新建文件 popen.php

```
[root@CentOS-76 html]# vim popen.php
```

```php
<?php
$test = "id";
$fp = popen($test,"r");
while (!feof($fp)) {
$out = fgets($fp, 4096);
echo $out;
}
pclose($fp);
?>
```

| 操作                      | 描述            |
| ----------------------- | ------------- |
| $fp = popen($test,"r"); | popen 打一个进程通道 |
| while (!feof($fp)) {    | 从通道里面取得东西     |
| echo $out;              | 打印出来          |

浏览器访问

> http://192.168.6.76/popen.php

输出

```
uid=48(apache) gid=48(apache) groups=48(apache)
```

### 3.1.9 proc_open()

新建文件 proc_open.php

```
[root@CentOS-76 html]# vim proc_open.php
```

```php
<?php
$test = "id";
$array = array(
array("pipe","r"),
array("pipe","w"),
array("pipe","w")
);
$fp = proc_open($test,$array,$pipes);
echo stream_get_contents($pipes[1]);
proc_close($fp);
?>
```

| 操作                                    | 描述                       |
| ------------------------------------- | ------------------------ |
| array("pipe","r"),                    | 标准输入                     |
| array("pipe","w"),                    | 标准输出内容                   |
| array("pipe","w")                     | 标准输出错误                   |
| $fp = proc_open($test,$array,$pipes); | 打开一个进程通道                 |
| echo stream_get_contents($pipes[1]);  | 为什么是$pipes[1]，因为 1 是输出内容 |

浏览器访问

> http://192.168.6.76/proc_open.php

输出

```
uid=48(apache) gid=48(apache) groups=48(apache) 
```

### 3.1.10 shell_exec()

新建文件 shell_exec.php

```
[root@CentOS-76 html]# vim shell_exec.php
```

```php
<?php
$test = "cat /etc/passwd";
$out = shell_exec($test);
echo $out;
?>
```

浏览器访问

> http://192.168.6.76/shell_exec.php

输出

```
root:x:0:0:root:/root:/bin/bash bin:x:1:1:bin:/bin:/sbin/nologin daemon:x:2:2:daemon:/sbin:/sbin/nologin adm:x:3:4:adm:/var/adm:/sbin/nologin lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin 
```

---

参考链接

- [PHP](https://www.php.net/downloads.php)
- [PHP Documentation](https://www.php.net/docs.php)
