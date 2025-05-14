Web 漏洞 POC 扫描工具.

## 1. 安装

安装

```
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

## 2. 初始化

更新模板

```
nuclei -update-templates
```

## 3. 使用

指定 PoC 验证目标漏洞

```
nuclei -u https://example.com -t fileName.yaml -je fileName.json
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

Refrences

- [nuclei](https://www.kali.org/tools/nuclei/)

