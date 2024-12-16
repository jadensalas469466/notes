用于探测未使用 CDN 的域名.

## 1. 部署

克隆仓库

```shell
root@debian:~# git clone https://github.com/jadensalas469466/cdnNone.git /root/tools/cdnNone && cd /root/tools/cdnNone
```

## 2. 初始化

编写运行脚本

```shell
root@debian:~/tools/cdnNone# vim ./cdnNone.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 cdnNone
python3 cdnNone.py "$@"
```

创建链接

```shell
root@debian:~/tools/cdnNone# chmod +x ./cdnNone.sh && ln -s /root/tools/cdnNone/cdnNone.sh /usr/local/bin/cdnNone && cd
```

查看帮助

```shell
root@debian:~# cdnNone
```

## 3. 使用

```shell
root@debian:~# cdnNone -d fileName.txt -o fileName.txt
```

---

参考链接

- [cdnNone](https://github.com/jadensalas469466/cdnNone)