Tor protects your privacy on the internet by hiding the connection between your Internet address and the services you use. We believe Tor is reasonably secure, but please ensure you read the instructions and configure it properly.

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ sudo apt install -y tor
```

## 2. Init

```
┌──(sec@debian)-[~]
└─$ sudo nano -l /etc/tor/torrc
```

```
MaxCircuitDirtiness 60
NewCircuitPeriod 60
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 80 127.0.0.1:80
```

重启并配置开机自启

```
┌──(sec@debian)-[~]
└─$ sudo systemctl restart tor.service && sudo systemctl enable tor.service
```

> 默认端口 127.0.0.1:9050

查看分配到的 Onion 域名

```
┌──(sec@debian)-[~]
└─$ sudo cat /var/lib/tor/hidden_service/hostname
```

```
example.onion
```

> Tor 会将来自 `example.onion` 的访问转发到本机的 80 端口

---

References

- [Tor](https://www.torproject.org/)
- [Tor support](https://support.torproject.org/)
- [Onion Services](https://support.torproject.org/onionservices/)

