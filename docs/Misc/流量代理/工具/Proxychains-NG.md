一个开源的命令行工具，用于将网络流量通过代理服务器转发。

## 1 安装

安装

```
┌──(root@debian)-[~]
└─# apt install -y proxychains4
```

## 2 初始化

修改配置文件

```
┌──(root@debian)-[~]
└─# vim /etc/proxychains4.conf
```

```
161  # socks4        127.0.0.1 9050
162  socks5          127.0.0.1 10808
```

测试代理

```
┌──(root@debian)-[~]
└─# proxychains4 curl ip.sb
```

## 3 使用

通过代理执行程序

```shell
┌──(root㉿kali)-[~]
└─# proxychains4 sqlmap -g "inurl:\".php?id=1\""
```

---

参考链接

- [Proxychains-NG](https://github.com/rofl0r/proxychains-ng)
