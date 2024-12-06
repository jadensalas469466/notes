一个匿名网络浏览工具。

## 1 部署

安装

```shell
┌──(root㉿kali)-[~]
└─# apt install -y tor
```

## 2 初始化

配置为每分钟切换一次代理链

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/tor/torrc
```

```
MaxCircuitDirtiness 60
NewCircuitPeriod 60
```

配置开机自启

```shell
┌──(root㉿kali)-[~]
└─# systemctl enable --now tor.service
```

> 默认端口 127.0.0.1:9050

---

参考链接

- [Tor](https://gitlab.torproject.org/tpo/core/tor)
- [Tor Project](https://www.torproject.org/)

