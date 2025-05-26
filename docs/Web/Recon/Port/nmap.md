Nmap is a utility for network exploration or security auditing.

## 1. install

安装

```
sudo apt install -y nmap
```

## 2. use

对单个目标进行端口扫描

```
nmap -T4 -Pn -p- -sV -O <host> -oN nmap_<host>.txt
```

对多个目标进行端口扫描

```
nmap -T4 -Pn -p- -sV -O -iL host.txt -oN nmap_host.txt
```

Bypass

```
nmap -T4 -Pn -p- -sV -O -f -D RND:10 <host> -oN nmap_<host>.txt
```

漏洞扫描

```
nmap --script=vuln <host> -oN result.txt
```

---

Refrences

- [nmap](https://www.kali.org/tools/nmap/)
