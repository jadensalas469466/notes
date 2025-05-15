Tor protects your privacy on the internet by hiding the connection between your Internet address and the services you use. We believe Tor is reasonably secure, but please ensure you read the instructions and configure it properly.

## 1. install

安装

```
apt install -y tor
```

## 2. init

配置为每分钟切换一次代理链

```
echo "MaxCircuitDirtiness 60" >> /etc/tor/torrc \
&& echo "NewCircuitPeriod 60" >> /etc/tor/torrc
```

配置开机自启

```
systemctl enable --now tor.service
```

> 默认端口 127.0.0.1:9050

---

Refrences

- [Tor](https://gitlab.torproject.org/tpo/core/tor)

