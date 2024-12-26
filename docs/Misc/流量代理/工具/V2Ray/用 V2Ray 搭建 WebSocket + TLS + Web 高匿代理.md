![搭建高匿代理](./../../../../../images/%E7%94%A8%20V2Ray%20%E6%90%AD%E5%BB%BA%20WebSocket%20+%20TLS%20+%20Web%20%E9%AB%98%E5%8C%BF%E4%BB%A3%E7%90%86/%E6%90%AD%E5%BB%BA%E9%AB%98%E5%8C%BF%E4%BB%A3%E7%90%86.svg)

1. 使用 TLS 加密 Websocket 流量，使其看起来像是普通的 HTTPS 流量。
2. 将 Web 服务器伪装为电脑请求的目标网站。
3. GFW 检测到正常的 HTTPS 流量且目标网站不在黑名单，放行。
4. Web 服务器解密 TLS，将解密后的 Websocket 流量转发给代理服务。
5. 代理服务访问真正的目标网站。

## 1 安装

### 1.1 服务端

使用 UFW 开放网站端口 3628

```shell
root@server:~# ufw allow 3628
```

安装服务

```shell
root@server:~# apt install -y v2ray caddy
```

运行服务并设置开机自启

```shell
root@server:~# systemctl enable --now v2ray.service caddy.service
```

下载配置生成脚本

```shell
root@server:~# wget https://raw.githubusercontent.com/jadensalas469466/tools/refs/heads/main/other/v2rayConfig.py
```

创建目录用于存储 TLS 密钥和证书

```shell
root@server:~# mkdir /etc/ssl/caddy
```

生成 TLS 密钥

```shell
root@server:~# openssl ecparam -genkey -name secp384r1 -out /etc/ssl/caddy/ssl-test.pem
```

修改密钥的权限

```shell
root@server:~# chmod 600 /etc/ssl/caddy/ssl-test.pem
```

生成 TLS 证书

```shell
root@server:~# openssl req -new -x509 -key /etc/ssl/caddy/ssl-test.pem -out /etc/ssl/caddy/ssl-test.crt -days 365000 -subj "/CN=202.38.95.17" -addext "subjectAltName = IP:202.38.95.17"
```

修改证书的权限

```shell
root@server:~# chmod 644 /etc/ssl/caddy/ssl-test.crt
```

将 TLS 证书复制到本地安装

```shell
root@local:~# scp root@server:/etc/ssl/caddy/ssl-test.crt /root/
```

### 1.2 客户端

**linux**

安装服务

```
┌──(root㉿kali)-[~]
└─# apt install -y v2ray
```

运行服务并设置开机自启

```
┌──(root㉿kali)-[~]
└─# systemctl enable --now v2ray.service
```

**windows**

安装 [v2rayN](https://github.com/2dust/v2rayN)

## 2 初始化

### 2.1 服务端

为 caddy 添加网站根目录访问权限

```shell
root@server:~# chown -R caddy:caddy /var/www/html
```

为 caddy 添加密钥和证书访问权限

```shell
root@server:~# chown caddy:caddy /etc/ssl/caddy/ssl-test.pem /etc/ssl/caddy/ssl-test.crt
```

使用脚本生成随机配置

```shell
root@server:~# python config_generator.py
```

```
网站端口: 3628
代理端口: 32348
用户ID: 7e880348-4558-442b-817b-f49008836ea7
路径: KxNZK72q
```

修改服务端 v2ray 配置文件

```shell
root@server:~# vim /etc/v2ray/config.json
```

```JSON
{
    "inbounds": [
        {
            "port": 32348,
            "listen": "127.0.0.1",
            "protocol": "vmess",
            "settings": {
                "clients": [
                    {
                        "id": "7e880348-4558-442b-817b-f49008836ea7",
                        "alterId": 64,
                        "security": "chacha20-poly1305"
                    }
                ]
            },
            "streamSettings": {
                "network": "ws",
                "wsSettings": {
                    "path": "/KxNZK72q"
                }
            }
        }
    ],
    "outbounds": [
        {
            "protocol": "freedom",
            "settings": {}
        }
    ]
}
```

重启 v2ray 服务

```shell
root@server:~# systemctl restart v2ray.service
```

修改 caddy 配置文件

```shell
root@server:~# vim /etc/caddy/Caddyfile
```

```
:3628	{
		log {
		output file /etc/caddy/caddy.log
		}
		
		encode gzip
		file_server
		root * /var/www/html
        
		php_fastcgi unix//run/php/php8.2-fpm.sock {
		env API_KEY 2TJOT-QYX6H-CALAW
		env API_HASH 9b86a596179be8e10a4a6684781ab14528c186a0
		env API_URL https://instancecontrol.com/
		}

		tls /etc/ssl/caddy/ssl-test.crt /etc/ssl/caddy/ssl-test.pem {
		protocols tls1.2 tls1.3
		ciphers TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256
		curves x25519
		}

		@v2ray_websocket {
		path /KxNZK72q
		header Connection Upgrade
		header Upgrade websocket
		}
		reverse_proxy @v2ray_websocket 127.0.0.1:32348
}
```

重启 caddy 服务

```shell
root@server:~# systemctl restart caddy.service
```

将证书复制到网站上传目录

```shell
root@linux:~# cp /etc/ssl/caddy/ssl-test.crt /var/www/html/upload/
```

下载证书并安装到本地

> https://example.com:3628/upload/ssl-test.crt

删除网站上传目录的证书

### 2.2 客户端

**linux**

修改客户端配置文件

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/v2ray/config.json
```

```

```

修改后重启服务

```shell
┌──(root㉿kali)-[~]
└─# systemctl restart v2ray.service
```

**windows**

```
VMess服务器
内核：Xray
别名：test
地址：202.38.95.17
端口：3628
用户ID：7e880348-4558-442b-817b-f49008836ea7
额外ID：64
加密方式：chacha20-poly1305

底层传输方式
传输协议：ws
伪装类型：none
伪装域名：202.38.95.17
路径：/KxNZK72q

传输层安全：tls
SNI：202.38.95.17
Fingerprint：chrome
Alpn：h2
跳过证书验证：true
```

> 注意添加防火墙规则

## 帮助

```shell
root@server:~# v2ray -h
```

```
Usage of v2ray:
  -c value
        -config 的简写
  -confdir 目录
        包含多个 JSON 配置文件的目录
  -config value
        V2Ray 的配置文件。可以指定多个（仅限 JSON）。后面的配置会覆盖前面的配置。
  -format string
        输入文件的格式。（默认 "json"）
  -test
        仅测试配置文件，不启动 V2Ray 服务器。
  -version
        显示 V2Ray 的当前版本。
```

---

参考链接

- [V2Fly](https://www.v2fly.org/)
- [WebSocket + TLS + Web](https://guide.v2fly.org/advanced/wss_and_web.html)

