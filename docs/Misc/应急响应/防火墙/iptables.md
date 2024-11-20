 Linux 防火墙。

## 1 使用

拦截来自特定 IP 地址的流量。

```shell
[root@centos ~]# iptables -A INPUT -s [ip] -j DROP
```

移除拦截规则

```shell
[root@centos ~]# iptables -D INPUT -s [ip] -j DROP
```

拦截本机发往特定 IP 地址的流量。

```shell
[root@centos ~]# iptables -A OUTPUT -d [ip] -j DROP
```

拦截所有主动向外发送的数据包（适用于应对反弹 shell 的木马）

```shell
[root@centos ~]# iptables -t filter -A OUTPUT -m state --state NEW -j DROP
```

解除所有规则

```shell
[root@centos ~]# iptables -F
```

---

参考链接

- [iptables](https://wiki.debian.org/iptables)
