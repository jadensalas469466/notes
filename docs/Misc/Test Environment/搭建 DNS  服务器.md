搭建私人 DNS 服务器，避免国际 DNS 服务器被 [GFW](https://zh.wikipedia.org/zh-hans/%E9%98%B2%E7%81%AB%E9%95%BF%E5%9F%8E) 污染.

## 1 部署

使用 UFW 开放 DNS 端口 53

```shell
root@server:~# ufw allow 53
```

安装 Bind9 用于部署 DNS 服务器

```shell
root@server:~# apt install -y bind9
```

配置 Bind9 转发上游 DNS

```shell
root@server:~# vim /etc/bind/named.conf.options
```

```
options {
    // 指定缓存文件目录，用于存储 DNS 数据和其他信息
    directory "/var/cache/bind";

    // 配置上游 DNS 服务器（转发器），用于解析无法在本地缓存的域名
    forwarders {
        8.8.8.8;  // Google Public DNS
        1.1.1.1;  // Cloudflare DNS
    };

    // 设置为只使用上游 DNS 服务器进行查询
    forward only;

    // 启用 DNSSEC 验证，自动处理 DNSSEC 签名的验证
    // 确保返回的 DNS 响应是经过验证的，防止 DNS 欺骗
    dnssec-validation auto;

    // 允许来自所有 IP 地址的查询
    // 这将使 DNS 服务器能够响应任何来源的查询请求
    allow-query { any; };
};
```

使 Bind9 开机自启

```shell
root@server:~# systemctl enable --now named.service
```

在本地计算机中验证 DNS 服务器是否可用

```shell
root@server:~# dig @[server_ip] x.com
```

```
; <<>> DiG 9.18.28-1~deb12u2-Debian <<>> @[server_ip] x.com
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 23540
;; flags: qr rd ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: cd04537cf471b49c010000006724b5dd6d45bd3d71559f06 (good)
;; QUESTION SECTION:
;x.com.                         IN      A

;; ANSWER SECTION:
x.com.                  1800    IN      A       104.244.42.65
x.com.                  1800    IN      A       104.244.42.1
x.com.                  1800    IN      A       104.244.42.193
x.com.                  1800    IN      A       104.244.42.129

;; Query time: 251 msec
;; SERVER: [server_ip]#53([server_ip]) (UDP)
;; WHEN: Fri Nov 01 19:05:01 CST 2024
;; MSG SIZE  rcvd: 126

root@debian:~# ping x.com -c3
PING x.com (104.244.42.129) 56(84) bytes of data.
^C
--- x.com ping statistics ---
3 packets transmitted, 0 received, 100% packet loss, time 2031ms
```

---

Refrences

- [BIND 9](https://gitlab.isc.org/isc-projects/bind9)
- [debian配置BIND DNS服务器](https://blog.csdn.net/qq_51470638/article/details/138235472)

