SolusVM 2 是一款服务器管理面板.

## 1 安装

安装依赖

```
root@server:~# apt install -y caddy php-fpm php-curl
```

运行中间件

```
root@server:~# systemctl enable --now caddy.service && systemctl enable --now php-fpm.service
```

## 2 初始化

获取 API 和 URL

![获取 API 和 URL](./../../../images/%E4%BD%BF%E7%94%A8%20SolusVM%202%20API%20%E8%8E%B7%E5%8F%96%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BF%A1%E6%81%AF/%E8%8E%B7%E5%8F%96%20API%20%E5%92%8C%20URL.png)

配置 API

```shell
root@server:~# vim /etc/caddy/Caddyfile
```

```
     6		encode gzip
     7		file_server
     8
     9		root * /var/www/html
    10		try_files {path} /index.php
    11
    12		php_fastcgi unix//run/php/php-fpm.sock {
    13		env API_KEY 2TJOT-QYX6H-CALAW
    14		env API_HASH 9b86a596179be8e10a4a6684781ab14528c186a0
    15		env API_URL https://instancecontrol.com/
    16		}
```

重启中间件

```shell
root@server:~# systemctl restart caddy
```

获取 PHP 脚本

```
root@server:~# curl -L https://raw.githubusercontent.com/jadensalas469466/tools/refs/heads/main/other/SolusVM%202/index.php -o /var/www/html/index.php
```

访问主页即可查看服务器状态

![访问主页即可查看服务器状态](./../../../images/%E4%BD%BF%E7%94%A8%20SolusVM%202%20API%20%E8%8E%B7%E5%8F%96%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BF%A1%E6%81%AF/%E8%AE%BF%E9%97%AE%E4%B8%BB%E9%A1%B5%E5%8D%B3%E5%8F%AF%E6%9F%A5%E7%9C%8B%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%8A%B6%E6%80%81.png)

---

参考链接

- [SolusVM 2 Documentation](https://docs.solusvm.com/)
- [Caddy Documentation](https://caddyserver.com/docs/)
