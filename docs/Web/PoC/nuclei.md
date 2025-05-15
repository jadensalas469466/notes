Nuclei is used to send requests across targets based on a template leading to zero false positives and providing fast scanning on large number of hosts. Nuclei offers scanning for a variety of protocols including TCP, DNS, HTTP, File, etc. With powerful and flexible templating, all kinds of security checks can be modelled with Nuclei.

## 1. install

安装

```
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

## 2. init

更新模板

```
nuclei -update-templates
```

## 3. use

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

