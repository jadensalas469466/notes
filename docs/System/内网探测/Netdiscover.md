地址侦查工具。

## 1 使用

查看手册

```shell
┌──(root㉿kali)-[~]
└─# man netdiscover
```

直接探测

```shell
┌──(root㉿kali)-[~]
└─# netdiscover
```

被动探测

```shell
┌──(root㉿kali)-[~]
└─# netdiscover -p
```

指定网卡

```shell
┌──(root㉿kali)-[~]
└─# netdiscover -i eth0
```

指定网段

```shell
┌──(root㉿kali)-[~]
└─# netdiscover -r 192.168.1.0/24
```

---

参考链接

- [Netdiscover](https://www.kali.org/tools/netdiscover/)
