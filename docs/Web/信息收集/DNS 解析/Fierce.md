DNS 侦查工具，用于定位非连续 IP 空间。

## 1 部署

安装

```shell
┌──(root㉿kali)-[~]
└─# python -m pip install fierce
```

## 2 使用

查看帮助

```shell
┌──(root㉿kali)-[~]
└─# fierce -h
```

扫描目标含有 `name` 的子域名

```shell
┌──(root㉿kali)-[~]
└─# fierce --domain [domain] --subdomains [name]
```

参考链接

- [Fierce](https://github.com/mschwager/fierce)
