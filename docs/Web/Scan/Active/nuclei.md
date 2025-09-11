Nuclei is a fast, customizable vulnerability scanner powered by the global security community and built on a simple YAML-based DSL, enabling collaboration to tackle trending vulnerabilities on the internet.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

## 2. Init

克隆模板

```
┌──(nemo@debian)-[~]
└─$ git clone https://github.com/projectdiscovery/nuclei-templates.git
```

更新程序和模板

```
┌──(nemo@debian)-[~]
└─$ nuclei -up && nuclei -ut
```

## 3. Usage

更新程序和模板

```
┌──(nemo@debian)-[~]
└─$ nuclei -up && nuclei -ut
```

经典扫描

```
┌──(nemo@debian)-[~]
└─$ nuclei -l host.txt -o nuclei_host.txt
```

指定 PoC 模板验证目标漏洞

```
┌──(nemo@debian)-[~]
└─$ nuclei -l host.txt -t ~/poc -o nuclei_host.txt
```

---

References

- [nuclei](https://github.com/projectdiscovery/nuclei)

