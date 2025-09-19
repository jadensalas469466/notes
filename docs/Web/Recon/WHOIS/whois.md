Intelligent WHOIS client.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y whois
```

## 2. Usage

查询 Registrant Organization

```
┌──(nemo@debian)-[~]
└─$ whois example.com | grep "Registrant Organization"
```

通过域名查询注册信息

```
┌──(nemo@debian)-[~]
└─$ whois example.com
```

通过 IP 查询归属组织

```
┌──(nemo@debian)-[~]
└─$ whois 1.1.1.1
```

---

References

- [whois](https://www.kali.org/tools/whois/)

