用于获取域名的 IP.

## 1. 安装

克隆仓库

```
┌──(root@debian)-[~]
└─# git clone https://github.com/jadensalas469466/ipGet.git /root/tools/apps/ipGet && cd /root/tools/apps/ipGet
```

## 2. 初始化

编写运行脚本

```
┌──(root@debian)-[~/tools/apps/ipGet]
└─# nano ./ipGet.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 ipGet
python3 ipGet.py "$@"
```

创建链接

```
┌──(root@debian)-[~/tools/apps/ipGet]
└─# chmod +x ./ipGet.sh && ln -s /root/tools/apps/ipGet/ipGet.sh /usr/local/bin/ipGet && cd
```

查看帮助

```
┌──(root@debian)-[~]
└─# ipGet
```

## 3. 使用

```
┌──(root@debian)-[~]
└─# ipGet -d fileName.txt -o fileName.txt
```

---

参考链接

- [ipGet](https://github.com/jadensalas469466/ipGet)

