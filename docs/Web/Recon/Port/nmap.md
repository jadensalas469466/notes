Nmap is a utility for network exploration or security auditing.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y nmap
```

## 2. Usage

> 系统检测需要扫描一个 `open` 端口和一个 `closed` 端口提高准确率

扫描单个目标的指定端口

```
┌──(nemo@debian)-[~]
└─$ sudo nmap -p 21,22,3306 -T4 -Pn -sV -O 1.1.1.1 -oN ~/nmap_1.1.1.1.txt
```

扫描多个目标的指定端口

```
┌──(nemo@debian)-[~]
└─$ sudo nmap -p 21,22,3306 -T4 -Pn -O -sV -iL ~/ip.txt -oN ~/nmap_host.txt
```

Bypass

```
┌──(nemo@debian)-[~]
└─$ sudo nmap -p 21,22,3306 -T4 -Pn -sV -O -f -D RND:10 1.1.1.1 -oN ~/nmap_1.1.1.1.txt
```

---

References

- [nmap](https://www.kali.org/tools/nmap/)
