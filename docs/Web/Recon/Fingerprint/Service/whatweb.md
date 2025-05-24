Identify the technology stack that powers a website and explore the Web of Things.

## 1. install

安装

```
apt install -y whatweb
```

## 2. use

识别单个目标使用的 Web 服务

```
whatweb -a 3 -v <host> --color=never > whatweb_<host>.txt
```

识别多个目标使用的 Web 服务

```
whatweb -a 3 -v --color=never -i host.txt > whatweb_host.txt
```

---

Refrences

- [whatweb](https://www.kali.org/tools/whatweb/)

