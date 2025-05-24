网络爬虫。

## 1 安装

下载

```shell
root@debian:~# wget https://github.com/Qianlitp/crawlergo/releases/download/v0.4.4/crawlergo_linux_amd64 -P /root/tools/crawlergo
```

编写脚本

```shell
root@debian:~# chmod +x /root/tools/crawlergo/crawlergo_linux_amd64 && vim /root/tools/crawlergo/crawlergo.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 crawlergo
./crawlergo_linux_amd64 "$@"
```

创建链接

```shell
root@debian:~# chmod +x /root/tools/crawlergo/crawlergo.sh && ln -s /root/tools/crawlergo/crawlergo.sh /usr/local/bin/crawlergo
```

## 2 使用

查看帮助

```shell
root@debian:~# crawlergo -h
```

对目标进行爬虫

```shell
root@debian:~# crawlergo [url]
```

---

Refrences

- [crawlergo](https://github.com/Qianlitp/crawlergo)
