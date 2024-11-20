通过 redsocks 将本机的 TCP 流量转发到 v2Ray。

## 1 初始化

修改配置文件

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/redsocks.conf
```

```
41 local_ip = 127.0.0.1;
42 local_port = 12345;
47 ip = 127.0.0.1;
48 port = 10808;
```

> 查看 redsocks 端口并添加代理服务器 IP 和端口

编写规则脚本

```shell
┌──(root㉿kali)-[~]
└─# mkdir /root/tool/proxy && vim /root/tool/proxy/ip-rules.sh
```

```sh
# 清空规则
iptables -t nat -F

# 服务端地址
iptables -t nat -A OUTPUT -d [server_ip] -j RETURN

# 过滤 ip
iptables -t nat -A OUTPUT -d 0.0.0.0/8 -j RETURN
iptables -t nat -A OUTPUT -d 10.0.0.0/8 -j RETURN
iptables -t nat -A OUTPUT -d 100.64.0.0/10 -j RETURN
iptables -t nat -A OUTPUT -d 127.0.0.0/8 -j RETURN
iptables -t nat -A OUTPUT -d 169.254.0.0/16 -j RETURN
iptables -t nat -A OUTPUT -d 172.16.0.0/12 -j RETURN
iptables -t nat -A OUTPUT -d 192.168.0.0/16 -j RETURN
iptables -t nat -A OUTPUT -d 198.18.0.0/15 -j RETURN
iptables -t nat -A OUTPUT -d 224.0.0.0/4 -j RETURN
iptables -t nat -A OUTPUT -d 240.0.0.0/4 -j RETURN

# redsocks 端口
iptables -t nat -A OUTPUT -p tcp -j REDIRECT --to-ports 12345
```

编写运行脚本

```shell
┌──(root㉿kali)-[~]
└─# vim /root/tool/proxy/proxy.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 显示脚本的使用说明函数
usage() {
    echo "Usage: $0 {-h|start|stop}"
    echo "       -h: 显示帮助信息"
    echo "    start: 启动 redsocks 服务并执行规则脚本"
    echo "     stop: 停止 redsocks 服务"
    exit 1
}

# 判断输入参数
case "$1" in
    start)
        # 启动 redsocks 服务
        systemctl start redsocks.service
        # 执行规则脚本
        sh ip-rules.sh
        ;;
    stop)
        # 停止 redsocks 服务
        systemctl stop redsocks.service
        # 清空规则
        iptables -t nat -F
        ;;
    -h)
        # 显示脚本的使用说明
        usage
        ;;
    *)
        # 如果输入参数不是 start、stop 或 -h，则显示用法说明并退出
        usage
        ;;
esac

# 退出脚本，返回状态码 0 表示成功
exit 0
```

创建链接

```shell
┌──(root㉿kali)-[~]
└─# chmod +x /root/tool/proxy/proxy.sh && ln -s /root/tool/proxy/proxy.sh /usr/local/bin/proxy
```

## 2 帮助

```
┌──(root㉿kali)-[~]
└─# proxy -h
```

```
Usage: /usr/local/bin/proxy {-h|start|stop}
       -h: 显示帮助信息
    start: 启动 redsocks 服务并执行规则脚本
     stop: 停止 redsocks 服务
```

---

参考链接

- [redsocks](https://github.com/darkk/redsocks)
- [redsocks Homepage](https://darkk.net.ru/redsocks/)

