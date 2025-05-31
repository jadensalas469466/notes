An advanced web path brute-forcer.

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ sudo apt install -y dirsearch
```

## 2. Usage

对单个目标进行经典扫描

```
┌──(sec@debian)-[~]
└─$ dirsearch -w ~/wordlist.txt -u https://example.com --format=plain -o ~/dirsearch_example.com.txt
```

对多个目标进行经典扫描

```
┌──(sec@debian)-[~]
└─$ dirsearch -w ~/wordlist.txt -l ~/url.txt --format=plain -o ~/dirsearch_url.txt
```

递归扫描两层

```
┌──(sec@debian)-[~]
└─$ dirsearch -w ~/wordlist.txt -l ~/url.txt -r -R 2 --format=plain -o ~/dirsearch_url.txt
```

扩展扫描

```
┌──(sec@debian)-[~]
└─$ dirsearch -w ~/wordlist_EXT.txt -e ~/wordlist.txt -l ~/url.txt --format=plain -o ~/dirsearch_url.txt
```

> `-e php,asp,jsp` , 添加指定扩展
>
> `-e ~/wordlist.txt` , 读取文件中的扩展
>
> 当字典中出现 `admin.%EXT%` 的行时自动爆破 `admin.php` ,  `admin.asp` ,  `admin.jsp` 
>
> 给没有 `.` 的行添加 `.%EXT%` : `sed '/\./! s/$/.%EXT%/' ~/wordlist.txt > ~/wordlist_EXT.txt` 

---

Refrences

- [dirsearch](https://www.kali.org/tools/dirsearch/)

