信息收集自动化工具.

## 1 部署

克隆项目

```shell
root@debian:~# git clone https://github.com/0x727/ShuiZe_0x727.git /root/tools/shuize && cd /root/tools/shuize
```

激活虚拟环境

```shell
root@debian:~/tools/shuize# python3 -m venv ./venv && source ./venv/bin/activate
```

执行安装脚本

```shell
(venv) root@debian:~/tools/shuize# chmod 777 ./build.sh && ./build.sh
```

查看帮助

```shell
(venv) root@debian:~/tools/shuize# python3 ./ShuiZe.py -h
```

退出虚拟环境

```shell
(venv) root@debian:~/tools/shuize# deactivate
```

## 2 初始化

编写运行脚本

```shell
root@debian:~/tools/shuize# vim ./shuize.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 激活虚拟环境
source /root/tools/shuize/venv/bin/activate

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 shuize
python3 ./ShuiZe.py "$@"
```

创建链接

```shell
root@debian:~/tools/shuize# chmod +x ./shuize.sh && ln -s /root/tools/shuize/shuize.sh /usr/local/bin/shuize && cd
```

查看帮助

```shell
root@debian:~# shuize -h
```

## 3 使用

单独收集根域名资产

```shell
root@debian:~# shuize -d example.com
```

批量收集根域名资产

```shell
root@debian:~# shuize --domainFile FileName.txt
```

---

参考链接

- [ShuiZe](https://github.com/0x727/ShuiZe_0x727)
