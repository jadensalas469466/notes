Proxychains is a UNIX program, that hooks network-related libc functions in dynamically linked programs via a preloaded DLL (dlsym(), LD_PRELOAD) and redirects the connections through SOCKS4a/5 or HTTP proxies. It supports TCP only (no UDP/ICMP etc).

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ sudo apt install -y proxychains4
```

## 2. Init

修改配置文件

```
┌──(sec@debian)-[~]
└─$ sudo nano -l /etc/proxychains4.conf
```

```
161  # socks5        127.0.0.1 9050
162  socks5          127.0.0.1 10808
```

测试代理

```
┌──(sec@debian)-[~]
└─$ proxychains4 curl ipinfo.io
```

## 3. Usage

通过代理执行程序

```
┌──(sec@debian)-[~]
└─$ proxychains4 <cmd>
```

---

References

- [proxychains-ng](https://www.kali.org/tools/proxychains-ng/)

