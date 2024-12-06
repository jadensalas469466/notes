## 1 Deploy

克隆项目

```shell
root@debian:~# git clone https://github.com/lijiejie/BBScan.git /root/tools/bbscan && cd /root/tools/bbscan
```

激活虚拟环境

```shell
(venv) root@debian:~/tools/bbscan# python -m venv ./venv && source ./venv/bin/activate
```

安装依赖

```shell
(venv) root@debian:~/tools/bbscan# python -m pip install -r requirements.txt
```

查看帮助

```shell
(venv) root@debian:~/tools/bbscan# python ./BBScan.py -h
```

退出虚拟环境

```shell
(venv) root@debian:~/tools/bbscan# deactivate
```

## 2 初始化

编写运行脚本

```shell
(venv) root@debian:~/tools/bbscan# vim ./bbscan.sh
```

```shell
#!/bin/bash

# 错误检测
set -e

# 激活虚拟环境
source /root/tools/bbscan/venv/bin/activate

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 bbscan
python ./BBScan.py "$@"
```

创建链接

```shell
root@debian:~/tools/bbscan# chmod +x ./bbscan.sh && ln -s /root/tools/bbscan/bbscan.sh /usr/local/bin/bbscan && cd
```

查看帮助

```shell
root@debian:~# bbscan -h
```

## 3 使用

从文件中扫描 URL 目标

```
bbscan -f /root/URLs.txt --api --no-browser
```

