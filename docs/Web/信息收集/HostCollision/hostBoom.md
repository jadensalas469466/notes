## 1 部署

克隆项目

```shell
root@debian:~# git clone https://github.com/fofapro/hostBoom.git /root/tools/apps && cd /root/tools/apps/hostBoom
```

激活虚拟环境

```shell
root@debian:~/tools/apps/hostBoom# python -m venv ./venv && source ./venv/bin/activate
```

安装依赖

```shell
(venv) root@debian:~/tools/apps/hostBoom# python -m pip install -r ./requirements.txt
```

查看帮助

```shell
(venv) root@debian:~/tools/apps/hostBoom# python ./hostBoom.py -h
```

退出虚拟环境

```shell
(venv) root@debian:~/tools/apps/hostBoom# deactivate
```

## 2 初始化

编写运行脚本

```shell
root@debian:~/tools/apps/hostBoom# vim ./hostBoom.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 激活虚拟环境
source /root/tools/apps/hostBoom/venv/bin/activate

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 hostBoom
python hostBoom.py "$@"
```

创建链接

```shell
root@debian:~/tools/apps/hostBoom# chmod +x ./hostBoom.sh && ln -s /root/tools/apps/hostBoom/hostBoom.sh /usr/local/bin/hostBoom && cd
```

查看帮助

```shell
root@debian:~# hostBoom --help
```

## 3 使用