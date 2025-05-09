用于探测未使用 CDN 的域名.

## 1. 安装

将脚本下载到本地

```
mkdir /root/tools/apps/cdn_none \
&& curl -L https://raw.githubusercontent.com/jadensalas469466/tools/refs/heads/main/hack/cdn_none.py -o /root/tools/apps/cdn_none/cdn_none.py
```

## 2. 初始化

编写运行脚本

```
nano /root/tools/apps/cdn_none/cdn_none.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 cdn_none
python3 cdn_none.py "$@"
```

创建链接

```
chmod +x /root/tools/apps/cdn_none/cdn_none.sh \
&& ln -s /root/tools/apps/cdn_none/cdn_none.sh /usr/local/bin/cdn_none
```

查看帮助

```
cdn_none
```

## 3. 使用

```
cdn_none -d fileName.txt -o fileName.txt
```

---

- [cdn_none.py](https://github.com/jadensalas469466/tools/blob/main/hack/cdn_none.py)