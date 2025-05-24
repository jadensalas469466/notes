Nuclei is a fast, customizable vulnerability scanner powered by the global security community and built on a simple YAML-based DSL, enabling collaboration to tackle trending vulnerabilities on the internet.

## 1. install

安装

```
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

## 2. init

克隆模板

```
git clone https://github.com/projectdiscovery/nuclei-templates.git
```

## 3. use

更新程序和模板

```
nuclei -up && nuclei -ut
```

经典扫描

```
nuclei -l host.txt -o nuclei_host.txt
```

指定 PoC 模板验证目标漏洞

```
nuclei -l host.txt -t /root/poc -o nuclei_host.txt
```

---

Refrences

- [nuclei](https://github.com/projectdiscovery/nuclei)

