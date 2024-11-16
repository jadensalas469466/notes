批量信息收集,供应链漏洞探测工具。

# 1 部署

下载

```shell
┌──(root㉿kali-23)-[~]
└─# mkdir /root/tools/dddd && proxychains4 curl -L 'https://github.com/SleepingBag945/dddd/releases/download/v2.0/dddd_linux64' -o /root/tools/dddd/dddd_linux64
```

编写脚本

```shell
┌──(root㉿kali-23)-[~]
└─# chmod +x /root/tools/dddd/dddd_linux64 && vim /root/tools/dddd/dddd.sh
```

```sh
#!/usr/bin/zsh

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 dddd
./dddd_linux64 "$@"

```

创建链接

```shell
┌──(root㉿kali)-[~]
└─# chmod +x /root/tools/dddd/dddd.sh && ln -s /root/tools/dddd/dddd.sh /usr/local/bin/dddd
```

# 2 初始化

配置 API

```shell
┌──(root㉿kali-23)-[~]
└─# dddd -t 127.0.0.1 -sd && vim /root/tools/dddd/config/api-config.yaml
```

# 3 使用

经典扫描

```shell
┌──(root㉿kali-23)-[~]
└─# dddd -t [host] -sd -ho result.html
```

# 4 帮助

```shell
┌──(root㉿kali-23)-[~]
└─# dddd -h
```

---

参考链接

- [dddd](https://github.com/SleepingBag945/dddd)
