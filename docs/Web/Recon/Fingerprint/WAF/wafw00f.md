The Web Application Firewall Fingerprinting Tool.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y wafw00f
```

## 2. Usage

识别单个目标使用的 WAF

```
┌──(nemo@debian)-[~]
└─$ wafw00f -a https://example.com -o ~/wafw00f_example.com.txt
```

识别多个目标使用的 WAF

```
┌──(nemo@debian)-[~]
└─$ wafw00f -a -i ~/url.txt -o ~/wafw00f_url.txt
```

---

References

- [wafw00f](https://www.kali.org/tools/wafw00f/)

