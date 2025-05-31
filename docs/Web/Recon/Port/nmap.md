Nmap is a utility for network exploration or security auditing.

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ sudo apt install -y nmap
```

## 2. Usage

> 系统监测需要扫描一个开放端口和一个关闭端口, 指定一个不常用的端口用于系统检测如: `65535`

扫描单个目标的指定端口

```
┌──(sec@debian)-[~]
└─$ sudo nmap -p 22,80,443,65535 -T4 -Pn -sV -O <host> -oN nmap_port.txt
```

扫描多个目标的指定端口

```
┌──(sec@debian)-[~]
└─$ sudo nmap -p 22,80,443,65535 -T4 -Pn -sV -O -iL host.txt -oN nmap_port.txt
```

Bypass

```
┌──(sec@debian)-[~]
└─$ sudo nmap -p 22,80,443,65535 -T4 -Pn -sV -O -f -D RND:10 <host> -oN nmap_port.txt
```

漏洞扫描

```
┌──(sec@debian)-[~]
└─$ sudo nmap --script=vuln <host> -oN nmap_port.txt
```

---

Refrences

- [nmap](https://www.kali.org/tools/nmap/)
