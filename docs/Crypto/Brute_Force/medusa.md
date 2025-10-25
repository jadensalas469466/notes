Medusa is intended to be a speedy, massively parallel, modular, login brute-forcer.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y medusa
```

## 2. Usage

列出已知模块

```
┌──(nemo@debian)-[~]
└─$ medusa -d
```

爆破 SSH

```
medusa -M ssh -h example.com -u username -p password -e ns

medusa -M ssh -H host.txt -U username.txt -P password.txt -e ns 
```

---

References

- [medusa](https://www.kali.org/tools/medusa/)
