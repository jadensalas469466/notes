用于获取域名的 IP.

## 1. 部署

克隆仓库

```shell
root@debian:~# git clone https://github.com/jadensalas469466/ipGet.git /root/tools/ipGet && cd /root/tools/ipGet
```

## 2. 初始化

编写运行脚本

```shell
root@debian:~/tools/ipGet# vim ./ipGet.sh
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

```shell
root@debian:~/tools/ipGet# chmod +x ./ipGet.sh && ln -s /root/tools/ipGet/ipGet.sh /usr/local/bin/ipGet && cd
```

查看帮助

```shell
root@debian:~# ipGet
```

## 3. 使用

```shell
root@debian:~# ipGet -d fileName.txt -o fileName.txt
```

---

参考链接

- [ipGet](https://github.com/jadensalas469466/ipGet)

