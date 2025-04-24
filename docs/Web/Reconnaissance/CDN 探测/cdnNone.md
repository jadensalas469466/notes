用于探测未使用 CDN 的域名.

## 1. 安装

将脚本下载到本地

```
mkdir /root/tools/apps/cdnNone \
&& curl -L https://raw.githubusercontent.com/jadensalas469466/tools/refs/heads/main/hack/cdnNone.py -o /root/tools/apps/cdnNone/cdnNone.py
```

## 2. 初始化

编写运行脚本

```
nano /root/tools/apps/cdnNone/cdnNone.sh
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

```
chmod +x /root/tools/apps/cdnNone/cdnNone.sh \
&& ln -s /root/tools/apps/cdnNone/cdnNone.sh /usr/local/bin/cdnNone
```

查看帮助

```
cdnNone
```

## 3. 使用

```
cdnNone -d fileName.txt -o fileName.txt
```

---

- [cdnNone](https://github.com/jadensalas469466/tools/blob/main/hack/cdnNone.py)