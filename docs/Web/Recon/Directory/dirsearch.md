An advanced web path brute-forcer.

## 1. Install

安装

```
sudo apt install -y dirsearch
```

## 2. Usage

对单个目标进行经典扫描

```
dirsearch -w /root/wordlist.txt -u https://example.com --format=plain -o /root/dirsearch_example.com.txt
```

对多个目标进行经典扫描

```
dirsearch -w /root/wordlist.txt -l /root/url.txt --format=plain -o /root/dirsearch_url.txt
```

递归扫描

```
dirsearch -w /root/wordlist.txt -l /root/url.txt -r --format=plain -o /root/dirsearch_example.com.txt
```

扩展扫描

```
dirsearch -w /root/wordlist.txt -e * -l /root/url.txt --format=plain -o /root/dirsearch_url.txt
```

> `-e *` , 以字典中出现的后缀添加扩展
>
> `-e php,asp,jsp`, 添加指定扩展
>
> 当字典中出现 `admin.%EXT%` 的行时自动爆破 `admin.php` ,  `admin.asp` ,  `admin.jsp` 
>
> 可使用 Vim:  `g/^[^\.]*$/s/$/.%EXT%/` 添加占位符 `.%EXT%/` 

---

Refrences

- [dirsearch](https://www.kali.org/tools/dirsearch/)

