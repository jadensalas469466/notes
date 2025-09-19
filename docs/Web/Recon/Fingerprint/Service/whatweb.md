Identify the technology stack that powers a website and explore the Web of Things.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y whatweb
```

## 2. Usage

识别单个目标使用的 Web 服务

```
┌──(nemo@debian)-[~]
└─$ whatweb -a 3 https://example.com/ --color=never | tee ~/whatweb_example.com.txt
```

识别多个目标使用的 Web 服务

```
┌──(nemo@debian)-[~]
└─$ whatweb -a 3 -i ~/url.txt --color=never | tee ~/whatweb_url.txt
```

---

References

- [whatweb](https://www.kali.org/tools/whatweb/)

