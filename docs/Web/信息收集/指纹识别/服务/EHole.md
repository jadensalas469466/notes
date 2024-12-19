Web 服务指纹识别工具.

## 1. 部署

下载

```shell
root@debian:~# curl -L -O https://github.com/EdgeSecurityTeam/EHole/releases/download/v3.1/EHole_linux_amd64.zip
```

解压

```shell
root@debian:~# unzip ./EHole_linux_amd64.zip -d ./tools/apps/ehole && rm -rf ./EHole_linux_amd64.zip && cd /root/tools/apps/ehole/EHole_linux_amd64
```

查看帮助

```shell
root@debian:~/tools/apps/ehole/EHole_linux_amd64# chmod +x ./EHole_linux_amd64 && ./EHole_linux_amd64 -h
```

## 2. 初始化

编写运行脚本

```shell
root@debian:~/tools/apps/ehole/EHole_linux_amd64# vim ./ehole.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 ehole
./EHole_linux_amd64 "$@"
```

创建链接

```shell
root@debian:~/tools/apps/ehole/EHole_linux_amd64# chmod +x ./ehole.sh && ln -s /root/tools/apps/ehole/EHole_linux_amd64/ehole.sh /usr/local/bin/ehole && cd
```

查看帮助

```shell
root@debian:~# ehole -h
```

## 3. 使用

识别目标使用的 Web 服务

```shell
root@debian:~# ehole finger -u <target-url> -o /path/fileName.json
```
