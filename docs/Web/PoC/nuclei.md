Nuclei is a fast, customizable vulnerability scanner powered by the global security community and built on a simple YAML-based DSL, enabling collaboration to tackle trending vulnerabilities on the internet.

## 1. install

安装

```
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

## 2. use

更新模板

```
nuclei -update-templates
```

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

