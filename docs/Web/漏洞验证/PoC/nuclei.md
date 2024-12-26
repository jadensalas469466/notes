Web 漏洞 POC 扫描工具。

## 1. 安装

安装

```
┌──(root@debian)-[~]
└─# sudo apt install -y nuclei
```

## 2. 使用

指定 PoC 验证目标漏洞

```
┌──(root@debian)-[~]
└─# nuclei -u https://example.com -t fileName.yaml -o fileName.txt
```

更新模板

```
┌──(root@debian)-[~]
└─# nuclei -update-templates
```

查看模板

```
┌──(root@debian)-[~]
└─#ls /root/.local/nuclei-templates
```

---

参考链接

- [nuclei](https://www.kali.org/tools/nuclei/)

