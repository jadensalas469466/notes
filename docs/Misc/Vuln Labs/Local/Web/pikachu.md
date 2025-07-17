一个好玩的Web安全-漏洞测试平台.

## 1. Install

安装依赖

```
┌──(sec@debian)-[~]
└─$ sudo apt install -y apache2 mariadb-server mariadb-client php php-mysqli
```

Clone

```
┌──(sec@debian)-[~]
└─$ sudo -E git clone https://github.com/zhuifengshaonianhanlu/pikachu.git /var/www/html/pikachu
```

## 2. Init

配置数据库密码

```
┌──(sec@debian)-[~]
└─$ sudo nano -l /var/www/html/pikachu/inc/config.inc.php
```

```php
10 define('DBUSER', 'root');//将root修改为连接mysql的用户名
11 define('DBPW', '123456');//将root修改为连接mysql的密码，如果改了还是连接不上，请先手动连接下你的数据库，确保数据库服务没问题在说!
```

```
┌──(sec@debian)-[~]
└─$ sudo nano -l /var/www/html/pikachu/pkxss/inc/config.inc.php
```

```php
10 define('DBUSER', 'root');//将root修改为连接mysql的用户名
11 define('DBPW', '123456');//将root修改为连接mysql的密码
```

Click `安装/初始化` 

> http://127.0.0.1:60080/pikachu/install.php

## 3. Usage

Visit

> http://127.0.0.1:60080/pikachu/index.php

---

References

- [pikachu](https://github.com/zhuifengshaonianhanlu/pikachu)
