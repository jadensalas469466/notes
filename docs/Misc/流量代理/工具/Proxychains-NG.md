一个开源的命令行工具, 用于将网络流量通过代理服务器转发.

## 1 安装

安装

```
apt install -y proxychains4
```

## 2 初始化

修改配置文件

```
vim /etc/proxychains4.conf
```

```
161  # socks4        127.0.0.1 9050
162  socks5          127.0.0.1 10808
```

测试代理

```
proxychains4 curl ip.sb
```

## 3 使用

通过代理执行程序

```
proxychains4 appRun
```

---

参考链接

- [Proxychains-NG](https://github.com/rofl0r/proxychains-ng)
