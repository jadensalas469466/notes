## 1. 安装

安装 xray 服务

```
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install
```

## 2. 初始化

配置客户端

```
nano /usr/local/etc/xray/config.json
```

重启 xray 服务

```
systemctl restart xray.service
```

测试代理

```
curl -x socks://127.0.0.1:10808 ip.sb && curl -x http://127.0.0.1:10808 ip.sb
```

---

参考链接

- [Xray](https://xtls.github.io/)