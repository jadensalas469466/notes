一个开源的命令行工具，用于将网络流量通过代理服务器转发。

## 1 部署

安装

```shell
┌──(root㉿kali)-[~]
└─# apt install -y proxychains4
```

## 2 初始化

修改配置文件

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/proxychains4.conf
```

```
 10  dynamic_chain
 18  # strict_chain
161  # socks4        127.0.0.1 9050
162  socks5          127.0.0.1 9050
```

重启网络服务并测试代理

```shell
root@debian:~# systemctl restart networking && systemctl restart networking && proxychains4 curl ip.sb
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
