检测存活站点的工具.

## 1. 安装

安装

```
┌──(root@debian)-[~]
└─# go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest
```

## 2. 使用

检测存活的站点

```
┌──(root@debian)-[~]
└─# httpx -l fileName.txt -o fileName.txt
```

---

参考链接

- [httpx](https://www.kali.org/tools/httpx-toolkit/)

