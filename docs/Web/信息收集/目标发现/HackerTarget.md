综合信息收集工具。

# 1 部署

安装

```shell
┌──(root㉿kali)-[~]
└─# git clone https://github.com/ismailtasdelen/hackertarget.git /root/tools/hackertarget && pip3 install /root/tools/hackertarget
```

编写脚本

```shell
┌──(root㉿kali)-[~]
└─# vim /root/tools/hackertarget/hackertarget.sh
```

```sh
#!/usr/bin/zsh

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 hackertarget
python3 hackertarget.py "$@"
```

创建链接

```shell
┌──(root㉿kali)-[~]
└─# chmod +x /root/tools/hackertarget/hackertarget.sh && ln -s /root/tools/hackertarget/hackertarget.sh /usr/local/bin/hackertarget
```

# 2 使用

查看帮助

```shell
┌──(root㉿kali)-[~]
└─# hackertarget -h
```

运行

```shell
┌──(root㉿kali)-[~]
└─# hackertarget
```

```
[1]		跟踪路由
[2]		Ping 测试
[3]		DNS 查询
[4]		反向 DNS
[5]		查找 DNS 主机
[6]		查找共享 DNS
[7]		区域传输
[8] 	Whois 查询
[9] 	IP 位置查询
[10] 	反向 IP 查询
[11]	TCP 端口扫描
[12]	子网查询
[13]	HTTP 头检查
[14]	提取页面链接
[15]	版本
[16]	退出

Which option number :
```

---

参考链接

- [HackerTarget](https://github.com/pyhackertarget/hackertarget)

