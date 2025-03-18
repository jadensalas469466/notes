用于获取域名的 IP.

## 1. 安装

将脚本下载到本地

```
mkdir /root/tools/apps/ipGet \
&& curl -L https://raw.githubusercontent.com/jadensalas469466/tools/refs/heads/main/hack/ipGet.py -o /root/tools/apps/ipGet/ipGet.py
```

## 2. 初始化

编写运行脚本

```
nano /root/tools/apps/ipGet/ipGet.sh
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
chmod +x /root/tools/apps/ipGet/ipGet.sh \
&& ln -s /root/tools/apps/ipGet/ipGet.sh /usr/local/bin/ipGet
```

查看帮助

```
ipGet
```

## 3. 使用

```
ipGet -d fileName.txt -o fileName.txt
```

---

参考链接

- [ipGet](https://github.com/jadensalas469466/tools/blob/main/hack/ipGet.py)

