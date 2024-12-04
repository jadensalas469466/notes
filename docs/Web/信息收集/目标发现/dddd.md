批量信息收集, 供应链漏洞探测工具.

## 1 部署

克隆项目

```shell
root@debian:~# mkdir -p /root/tools/dddd/ && cd /root/tools/dddd/ && wget -O https://github.com/SleepingBag945/dddd/releases/download/v2.0.1/dddd_linux64
```

释放配置文件

```shell
root@debian:~/tools/dddd# chmod +x ./dddd_linux64 && ./dddd_linux64 -t 127.0.0.1
```

## 2 初始化

配置 API

```shell
root@debian:~/tools/dddd# vim ./config/api-config.yaml
```

编写运行脚本

```shell
root@debian:~/tools/dddd# vim ./dddd.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 dddd
./dddd_linux64 "$@"

```

创建链接

```shell
root@debian:~/tools/dddd# chmod +x ./dddd.sh && ln -s /root/tools/dddd/dddd.sh /usr/local/bin/dddd && cd
```

查看帮助

```shell
root@debian:~# dddd -h
```

## 3 使用

经典扫描

```shell
root@debian:~# dddd -t example.com
```

---

参考链接

- [dddd](https://github.com/SleepingBag945/dddd)
