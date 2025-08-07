Web 漏洞 POC 扫描工具.

## 1. 安装

下载

```
┌──(root㉿kali-23)-[~]
└─# curl -L https://github.com/veo/vscan/releases/download/v2.1.0/vscan_2.1.0_linux_amd64.zip -o /root/vscan_2.1.0_linux_amd64.zip
```

解压

```
┌──(root㉿kali-23)-[~]
└─# mkdir /root/tools/vscan && unzip /root/vscan_2.1.0_linux_amd64.zip -d /root/tools/vscan && rm -rf /root/vscan_2.1.0_linux_amd64.zip
```

编写脚本

```
┌──(root㉿kali)-[~]
└─# vim /root/tools/vscan/vscan.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 vscan
./vscan "$@"

```

创建链接

```
┌──(root㉿kali)-[~]
└─# chmod +x /root/tools/vscan/vscan.sh && ln -s /root/tools/vscan/vscan.sh /usr/local/bin/vscan
```

## 2. 使用

扫描 host

```shell
┌──(root㉿kali-23)-[~]
└─# vscan -host [host1,host2,host3...]
```

扫描 host 文件

```
┌──(root㉿kali-23)-[~]
└─# vscan -l [/root/hosts.txt]
```

---

References

- [vscan](https://github.com/veo/vscan)
