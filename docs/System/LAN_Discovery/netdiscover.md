Netdiscover is an active/passive address reconnaissance tool, mainly developed for those wireless networks without dhcp server, when you are wardriving. It can be also used on hub/switched networks.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y netdiscover
```

## 2. Usage

直接探测

```
┌──(nemo@debian)-[~]
└─$ sudo netdiscover
```

被动探测

```
┌──(nemo@debian)-[~]
└─$ sudo netdiscover -p
```

指定网卡

```
┌──(nemo@debian)-[~]
└─$ sudo netdiscover -i vboxnet0
```

指定网段

```
┌──(nemo@debian)-[~]
└─$ sudo netdiscover -r 192.168.1.0/24
```

---

References

- [netdiscover](https://www.kali.org/tools/netdiscover/)
