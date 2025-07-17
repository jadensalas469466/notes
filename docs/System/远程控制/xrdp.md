开源的 RDP 软件.

## 1. 安装

安装 xrdp

```
┌──(root㉿kali)-[~]
└─# apt install -y xrdp
```

## 2. 初始化

配置开机自启

```shell
┌──(root㉿kali)-[~]
└─# systemctl enable --now xrdp
```

> 每个账户只允许有一处登录

---

References

- [xrdp](https://www.xrdp.org/)

