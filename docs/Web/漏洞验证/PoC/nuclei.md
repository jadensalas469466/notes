Web 漏洞 POC 扫描工具.

## 1. 安装

安装

```
┌──(root@debian)-[~]
└─# go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

## 2. 使用

指定 PoC 验证目标漏洞

```
nuclei -u https://example.com -t fileName.yaml -o fileName.txt
```

更新模板

```
nuclei -update-templates
```

查看模板

```
ls /root/.local/nuclei-templates
```

---

参考链接

- [nuclei](https://www.kali.org/tools/nuclei/)

