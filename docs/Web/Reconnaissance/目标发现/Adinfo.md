通过访问目标的 `389` 端口（`LDAP` 服务）获取域信息。

## 1 安装

下载

```shell
┌──(root㉿kali)-[~]
└─# proxychains4 wget https://github.com/lzzbb/Adinfo/releases/download/v0.3/Adinfo_linux -P /root/tools/adinfo
```

编写脚本

```shell
┌──(root㉿kali)-[~]
└─# chmod +x /root/tools/adinfo/Adinfo_linux && vim /root/tools/adinfo/adinfo.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 adinfo
./Adinfo_linux "$@"
```

创建链接

```shell
┌──(root㉿kali)-[~]
└─# chmod +x /root/tools/adinfo/adinfo.sh && ln -s /root/tools/adinfo/adinfo.sh /usr/local/bin/adinfo
```

## 2 使用

查看帮助

```shell
┌──(root㉿kali)-[~]
└─# adinfo -h
```

查看域内所有的 `adcs` 信息

```shell
┌──(root㉿kali)-[~]
└─# adinfo -d redteam.lab --dc [ip] -u [username] -p [password] --getADCS
```

收集域内所有的 `dns` 信息

```shell
┌──(root㉿kali)-[~]
└─# adinfo -d redteam.lab --dc [ip] -u [username] -p [password] --getAllDNS
```

获取域内所有的用户名

```shell
┌──(root㉿kali)-[~]
└─# adinfo -d redteam.lab --dc [ip] -u [username] -p [password] --getUsefulUserName
```

---

参考链接

- [Adinfo](https://github.com/lzzbb/Adinfo)
