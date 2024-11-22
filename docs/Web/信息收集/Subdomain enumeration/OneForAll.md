OneForAll是一款功能强大的子域收集工具。

## 1 部署

配置 Python 虚拟环境 [virtualenv](https://keithpeck177271.gitbook.io/notes/misc/shi-yan-huan-jing/bian-cheng-yu-yan/jiao-ben/python/virtualenv)

克隆项目

```shell
root@debian:~# git clone https://github.com/shmilylty/OneForAll.git /root/tools/oneforall
```

创建虚拟环境

```shell
root@debian:~# virtualenv /root/tools/oneforall/venv
```

激活虚拟环境

```shell
root@debian:~# source /root/tools/oneforall/venv/bin/activate
```

升级 Python 工具包

```shell
(venv) root@debian:~# python3 -m pip install -U pip setuptools wheel
```

安装依赖

```shell
(venv) root@debian:~# pip3 install -r /root/tools/oneforall/requirements.txt
```

查看帮助

```shell
(venv) root@debian:~# python3 /root/tools/oneforall/oneforall.py --help
```

## 2 初始化

编写运行脚本

```shell
root@debian:~# vim /root/tools/oneforall/oneforall.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 激活虚拟环境
source /root/tools/oneforall/venv/bin/activate

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 oneforall
python3 oneforall.py "$@"
```

创建链接

```shell
root@debian:~# chmod +x /root/tools/oneforall/oneforall.sh && ln -s /root/tools/oneforall/oneforall.sh /usr/local/bin/oneforall
```

查看帮助

```shell
root@debian:~# oneforall --help
```

## 3 使用

枚举单个目标的子域名

```shell
root@debian:~# oneforall --target [host] run
```

枚举文件中所有目标的子域名

```shell
root@debian:~# oneforall --target [file].txt run
```

查看结果

```shell
root@debian:~# ls /root/tools/oneforall/results/
```

下载结果到本地查看

```powershell
PS C:\Users\sec> scp -r root@debian.attack:/root/tools/oneforall/results/ C:\Users\sec\Downloads\
```

