信息收集自动化工具.

## 1 部署

克隆项目

```shell
root@debian:~# git clone https://github.com/0x727/ShuiZe_0x727.git /root/tools/shuize
```

修改安装脚本的权限

```shell
root@debian:~# cd /root/tools/shuize && chmod 777 ./build.sh
```

创建虚拟环境

```shell
root@attack:~/tools/shuize# python3 -m venv ./venv && source ./venv/bin/activate
```

执行安装脚本

```shell
(venv) root@attack:~/tools/shuize# ./build.sh
```

查看帮助

```shell
(venv) root@attack:~/tools/shuize# python3 ./ShuiZe.py -h
```

退出虚拟环境

```shell
(venv) root@attack:~/tools/shuize# deactivate && cd
```

## 2 初始化

```shell
root@debian:~# vim /root/tools/shuize/shuize.sh
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
root@debian:~# chmod +x /root/tools/shuize/shuize.sh && ln -s /root/tools/shuize/shuize.sh /usr/local/bin/shuize
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
