OneForAll是一款功能强大的子域收集工具。

## 1 部署

克隆项目

```shell
root@debian:~# git clone https://github.com/shmilylty/OneForAll.git /root/tools/oneforall && cd /root/tools/oneforall
```

激活虚拟环境

```shell
root@debian:~/tools/oneforall# python3 -m venv ./venv && source ./venv/bin/activate
```

安装依赖

```shell
(venv) root@debian:~/tools/oneforall# python3 -m pip install -r ./requirements.txt
```

查看帮助

```shell
(venv) root@debian:~/tools/oneforall# python3 ./oneforall.py --help
```

退出虚拟环境

```shell
(venv) root@debian:~/tools/oneforall# deactivate
```

## 2 初始化

编写运行脚本

```shell
root@debian:~/tools/oneforall# vim ./oneforall.sh
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
root@debian:~/tools/oneforall# chmod +x ./oneforall.sh && ln -s /root/tools/oneforall/oneforall.sh /usr/local/bin/oneforall && cd
```

查看帮助

```shell
root@debian:~# oneforall --help
```

## 3 使用

枚举单个目标的子域名

```shell
root@debian:~# oneforall --target example.com run
```

枚举文件中所有目标的子域名

```shell
root@debian:~# oneforall --target FileName.txt run
```

查看结果

```shell
root@debian:~# ls /root/tools/oneforall/results/
```

下载结果到本地查看

```powershell
PS C:\Users\sec> scp -r root@debian:/root/tools/oneforall/results/ C:\Users\sec\Downloads\
```

