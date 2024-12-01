一个匿名网络浏览工具。

## 1 部署

安装

```shell
┌──(root㉿kali)-[~]
└─# apt install -y tor
```

## 2 使用

启动

```shell
┌──(root㉿kali)-[~]
└─# systemctl enable --now tor.service
```

> 默认端口 127.0.0.1:9050

## 3 配置

修改为每分钟切换一次代理链

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/tor/torrc
```

```
MaxCircuitDirtiness 60
NewCircuitPeriod 60
```

---

参考链接

- [Tor](https://gitlab.torproject.org/tpo/core/tor)
- [Tor Project](https://www.torproject.org/)

