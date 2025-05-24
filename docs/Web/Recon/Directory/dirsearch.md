An advanced web path brute-forcer.

## 1. install

安装

```
apt install -y dirsearch
```

## 2. use

对单个目标进行经典扫描

```
dirsearch -u https://example.com --format=plain -o /root/dirsearch_example.com.txt
```

对多个目标进行经典扫描

```
dirsearch -l url.txt --format=plain -o /root/dirsearch_url.txt
```

递归扫描

```
dirsearch -u https://example.com -r --format=plain -o /root/dirsearch_example.com.txt
```

---

Refrences

- [dirsearch](https://www.kali.org/tools/dirsearch/)

