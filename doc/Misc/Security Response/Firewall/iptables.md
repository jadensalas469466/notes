Iptables provides packet filtering, network address translation (NAT) and other packet mangling.

## 1. use

拦截来自特定 IP 地址的流量。

```
iptables -A INPUT -s <ip> -j DROP
```

移除拦截规则

```
iptables -D INPUT -s <ip> -j DROP
```

拦截本机发往特定 IP 地址的流量。

```
iptables -A OUTPUT -d <ip> -j DROP
```

拦截所有主动向外发送的数据包（适用于应对反弹 shell 的木马）

```
iptables -t filter -A OUTPUT -m state --state NEW -j DROP
```

解除所有规则

```
iptables -F
```

---

References

- [iptables](https://wiki.debian.org/iptables)
