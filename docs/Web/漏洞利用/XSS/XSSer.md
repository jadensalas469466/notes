XSS Fuzz。

# 1 部署

安装

```shell
┌──(root㉿kali)-[~]
└─# sudo apt install -y python3-selenium && sudo apt install -y xsser
```

# 2 使用

查看帮助

```shell
┌──(root㉿kali)-[~]
└─# xsser -h
```

使用 `xsser` 对目标进行漏洞扫描

```shell
┌──(root㉿kali)-[~]
└─# xsser -u [url] -c 100 --Cl -p [xss]
```

---

参考链接

- [XSSer](https://www.kali.org/tools/xsser/)
