This is an Internet-scale port scanner. It can scan the entire Internet in under 5 minutes, transmitting 10 million packets per second, from a single machine.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y masscan
```

## 2. Usage

对单个目标进行全端口扫描

```
┌──(nemo@debian)-[~]
└─$ sudo masscan -p- <ip> -oL masscan_port.txt
```

对多个目标进行全端口扫描

```
┌──(nemo@debian)-[~]
└─$ sudo masscan -p- -iL ip.txt -oL masscan_port.txt
```

---

References

- [masscan](https://www.kali.org/tools/masscan/)