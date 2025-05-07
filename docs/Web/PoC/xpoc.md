Web 漏洞 POC 扫描工具.

## 1. 安装

下载

```
┌──(root@debian)-[~]
└─# curl -L https://github.com/chaitin/xpoc/releases/download/0.1.0/xpoc_linux_amd64.zip -o ./xpoc_linux_amd64.zip
```

解压

```
┌──(root@debian)-[~]
└─# unzip xpoc_linux_amd64.zip -d /root/tools/apps/xpoc \
&& rm -rf ./xpoc_linux_amd64.zip
```

编写运行脚本

```
┌──(root@debian)-[~]
└─# chmod +x /root/tools/apps/xpoc/xpoc_linux_amd64 \
&& vim /root/tools/apps/xpoc/xpoc.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 xpoc
./xpoc_linux_amd64 "$@"
```

创建链接

```
┌──(root@debian)-[~]
└─# chmod +x /root/tools/apps/xpoc/xpoc.sh \
&& ln -s /root/tools/apps/xpoc/xpoc.sh /usr/local/bin/xpoc
```

同步最新插件

```
┌──(root@debian)-[~]
└─# xpoc pull
```

## 2. 使用

扫描指定目标

```
┌──(root@debian)-[~]
└─# xpoc -t https://example.com -o /root/xpocScan.json
```

更新

```
┌──(root@debian)-[~]
└─# xpoc upgrade \
&& xpoc pull
```

---

参考链接

- [xpoc](https://github.com/chaitin/xpoc)
