Nmap is a utility for network exploration or security auditing.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y nmap
```

## 2. Usage

> 系统监测需要扫描一个开放端口和一个关闭端口, 指定一个不常用的端口用于系统检测如: `65535` 

扫描单个目标的指定端口

```
┌──(nemo@debian)-[~]
└─$ sudo nmap -p <prot1,port2...> -T4 -Pn -sV -O <host> -oN nmap_port.txt
```

扫描多个目标的指定端口

```
┌──(nemo@debian)-[~]
└─$ sudo nmap -p <prot1,port2...> -T4 -Pn -sV -O -iL host.txt -oN nmap_port.txt
```

Bypass

```
┌──(nemo@debian)-[~]
└─$ sudo nmap -p <prot1,port2...> -T4 -Pn -sV -O -f -D RND:10 <host> -oN nmap_port.txt
```

查看相关脚本

```
┌──(nemo@debian)-[~]
└─$ ls /usr/share/nmap/scripts/
```

漏洞扫描

```
┌──(nemo@debian)-[~]
└─$ sudo nmap -p <port> --script "<vuln>*" -d <host> -oN nmap_port.txt
```

---

References

- [nmap](https://www.kali.org/tools/nmap/)
