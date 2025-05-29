搭建私人 DNS 服务器，避免国际 DNS 服务器被 [GFW](https://github.com/gfwlist/gfwlist) 污染.

## 1. Deply

使用 UFW 开放 DNS 端口 53

```
┌──(sec@debian)-[~]
└─# sudo ufw allow 53
```

安装 Bind9 用于部署 DNS 服务器

```
┌──(sec@debian)-[~]
└─# sudo apt install -y bind9
```

配置 Bind9 转发上游 DNS

```
┌──(sec@debian)-[~]
└─# sudo nano /etc/bind/named.conf.options
```

```
options {
    // Specify the directory for cache files, used to store DNS data and other information
    directory "/var/cache/bind";

    // Configure upstream DNS servers (forwarders) to resolve domains not cached locally
    forwarders {
        8.8.8.8;  // Google Public DNS
        1.1.1.1;  // Cloudflare DNS
    };

    // Set to only use the upstream DNS servers for queries
    forward only;

    // Enable DNSSEC validation, automatically handling verification of DNSSEC signatures
    // Ensures that DNS responses are verified to prevent DNS spoofing
    dnssec-validation auto;

    // Allow queries from any IP address
    // This enables the DNS server to respond to queries from any source
    allow-query { any; };
};

```

使 Bind9 开机自启

```
┌──(sec@debian)-[~]
└─# sudo systemctl enable --now named.service
```

在本地计算机中验证 DNS 服务器是否可用

```
┌──(sec@debian)-[~]
└─# dig @<dns_ip> mit.edu
```

---

Refrences

- [BIND 9](https://gitlab.isc.org/isc-projects/bind9)
- [debian配置BIND DNS服务器](https://blog.csdn.net/qq_51470638/article/details/138235472)

