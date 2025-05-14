proxychains ng (new generation) - a preloader which hooks calls to sockets in dynamically linked programs and redirects it through one or more socks/http proxies.

## 1. install

安装

```
apt install -y proxychains4
```

## 2. init

修改配置文件

```
vim /etc/proxychains4.conf
```

```
161  # socks5        127.0.0.1 9050
162  socks5          127.0.0.1 10808
```

测试代理

```
proxychains4 curl ip.sb
```

## 3. use

通过代理执行程序

```
proxychains4 <app_run>
```

---

Refrences

- [Proxychains-NG](https://www.kali.org/tools/proxychains-ng/)

