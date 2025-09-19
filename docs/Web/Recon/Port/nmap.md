Nmap is a utility for network exploration or security auditing.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y nmap
```

## 2. Usage

> 系统检测至少需要扫描一个开放端口和一个关闭端口, 建议指定一个不常用的端口, 如: `65535` 

扫描单个目标的指定端口

```
┌──(nemo@debian)-[~]
└─$ sudo nmap -p 21,22,3306 -T4 -Pn -sV 1.1.1.1 -oN ~/nmap_1.1.1.1.txt
```

扫描多个目标的指定端口

```
┌──(nemo@debian)-[~]
└─$ sudo nmap -p 21,22,3306 -T4 -Pn -sV -iL ~/ip.txt -oN ~/nmap_host.txt
```

Bypass

```
┌──(nemo@debian)-[~]
└─$ sudo nmap -p 21,22,3306 -T4 -Pn -sV -f -D RND:10 1.1.1.1 -oN ~/nmap_1.1.1.1.txt
```

---

References

- [nmap](https://www.kali.org/tools/nmap/)
