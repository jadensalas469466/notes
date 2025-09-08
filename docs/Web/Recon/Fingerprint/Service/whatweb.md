Identify the technology stack that powers a website and explore the Web of Things.

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ sudo apt install -y whatweb
```

## 2. Usage

识别单个目标使用的 Web 服务

```
┌──(sec@debian)-[~]
└─$ whatweb -a 3 -v <host> --color=never > whatweb_<host>.txt
```

识别多个目标使用的 Web 服务

```
┌──(sec@debian)-[~]
└─$ whatweb -a 3 -v --color=never -i host.txt > whatweb_url.txt
```

---

References

- [whatweb](https://www.kali.org/tools/whatweb/)

