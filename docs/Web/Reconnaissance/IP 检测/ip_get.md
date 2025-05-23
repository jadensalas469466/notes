用于获取域名的 IP.

## 1. Install

将脚本下载到本地

```
mkdir /root/tools/apps/ip_get \
&& curl -L https://raw.githubusercontent.com/jadensalas469466/tools/refs/heads/main/hack/ip_get.py -o /root/tools/apps/ip_get/ip_get.py
```

## 2. 初始化

编写运行脚本

```
nano /root/tools/apps/ip_get/ip_get.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 ip_get
python3 ip_get.py "$@"
```

创建链接

```
chmod +x /root/tools/apps/ip_get/ip_get.sh \
&& ln -s /root/tools/apps/ip_get/ip_get.sh /usr/local/bin/ip_get
```

查看帮助

```
ip_get
```

## 3. Use

```
ip_get -d fileName.txt -o fileName.txt
```

---

Refrences

- [ip_get.py](https://github.com/jadensalas469466/tools/blob/main/hack/ip_get.py)

