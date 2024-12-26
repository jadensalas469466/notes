一个匿名网络浏览工具.

## 1 安装

安装

```
┌──(root@debian)-[~]
└─# apt install -y tor
```

## 2 初始化

配置为每分钟切换一次代理链

```
┌──(root@debian)-[~]
└─# echo 'MaxCircuitDirtiness 60' >> /etc/tor/torrc \
&& echo 'NewCircuitPeriod 60' >> /etc/tor/torrc
```

配置开机自启

```
┌──(root@debian)-[~]
└─# systemctl enable --now tor.service
```

> 默认端口 127.0.0.1:9050

---

参考链接

- [Tor](https://gitlab.torproject.org/tpo/core/tor)
- [Tor Project](https://www.torproject.org/)

