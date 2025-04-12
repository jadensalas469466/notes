暴力破解。

## 1 使用

爆破 ftp

```shell
┌──(root㉿kali-23)-[~]
└─# hydra [ip] ftp -l [usernamedict] -P [passworddict] -e ns -vV
```

## 2 帮助

```shell
┌──(root㉿kali-23)-[~]
└─# hydra -h
```

```
语法: hydra [[[-l 登录名|-L 文件] [-p 密码|-P 文件]] | [-C 文件]] [-e nsr] [-o 文件] [-t 任务数] [-M 文件 [-T 任务数]] [-w 时间] [-W 时间] [-f] [-s 端口] [-x 最小:最大:字符集] [-c 时间] [-ISOuvVd46] [-m 模块选项] [服务://服务器[:端口][/选项]]

选项:
  -R        恢复先前中止/崩溃的会话
  -I        忽略现有的恢复文件 (不等待10秒)
  -S        执行SSL连接
  -s 端口   如果服务在不同的默认端口上，请在此处定义
  -l 登录名 或 -L 文件  使用登录名登录，或从文件中加载多个登录名
  -p 密码 或 -P 文件  尝试密码，或从文件中加载多个密码
  -x 最小:最大:字符集  密码暴力生成，输入 "-x -h" 获取帮助
  -y        禁用密码暴力中的符号，请参见上文
  -r        对 -x 选项使用非随机洗牌方法
  -e nsr    尝试 "n" 空密码，"s" 作为密码登录和/或 "r" 反向登录
  -u        循环用户，而不是密码（有效！与 -x 隐含使用）
  -C 文件   以冒号分隔的 "登录名:密码" 格式，而不是 -L/-P 选项
  -M 文件   要攻击的服务器列表，每行一个条目，':' 指定端口
  -o 文件   将找到的登录名/密码对写入文件，而不是标准输出
  -b 格式   指定 -o 文件的格式: 文本(默认), json, jsonv1
  -f / -F   找到登录名/密码对时退出 (-M: -f 每个主机，-F 全局)
  -t 任务数  每个目标并行运行的连接数 (默认: 16)
  -T 任务数  总体并行运行的连接数（对于 -M，默认值: 64）
  -w / -W 时间  等待响应的时间 (32) / 线程间连接之间的等待时间 (0)
  -c 时间   每个线程上的登录尝试等待时间 (强制执行 -t 1)
  -4 / -6   使用IPv4 (默认) / IPv6地址（在 -M 中也始终使用 []）
  -v / -V / -d  详细模式 / 显示每次尝试的登录+密码 / 调试模式 
  -O        使用旧的SSL v2和v3
  -K        不重试失败的尝试（用于 -M 大规模扫描很好）
  -q        不打印有关连接错误的消息
  -U        服务模块使用详细信息
  -m 选项   特定于模块的选项，请参阅 -U 输出以获取信息
  -h        更多命令行选项（完整帮助）
  server    目标: DNS、IP或192.168.0.0/24（这个或 -M 选项）
  service   要破解的服务（支持的协议见下文）
  OPT       一些服务模块支持附加输入（-U 用于模块帮助）

支持的服务: adam6500 asterisk cisco cisco-enable cobaltstrike cvs firebird ftp[s] http[s]-{head|get|post} http[s]-{get|post}-form http-proxy http-proxy-urlenum icq imap[s] irc ldap2[s] ldap3[-{cram|digest}md5][s] memcached mongodb mssql mysql nntp oracle-listener oracle-sid pcanywhere pcnfs pop3[s] postgres radmin2 rdp redis rexec rlogin rpcap rsh rtsp s7-300 sip smb smtp[s] smtp-enum snmp socks5 ssh sshkey svn teamspeak telnet[s] vmauthd vnc xmpp

Hydra是一个猜测/破解有效登录名/密码对的工具。
根据AGPL v3.0许可。最新版本始终可在以下位置获取:
https://github.com/vanhauser-thc/thc-hydra
请不要在军事或秘密服务组织中使用，也不要用于非法目的。
（这是一个愿望，非约束性的 - 大多数这样的人都不关心法律和道德 - 并告诉自己他们是好人之一。）
这些服务未被编译进来: afp ncp oracle sapr3 smb2。

使用HYDRA_PROXY_HTTP或HYDRA_PROXY环境变量进行代理设置。
例如 % export HYDRA_PROXY=socks5://l:p@127.0.0.1:9150 (或: socks4:// connect://)
     % export HYDRA_PROXY=connect_and_socks_proxylist.txt  (最多64个条目)
     % export HYDRA_PROXY_HTTP=http://login:pass@proxy:8080
     % export HYDRA_PROXY_HTTP=proxylist.txt  (最多64个条目)

示例:
  hydra -l 用户名 -P 密码列表.txt ftp://192.168.0.1
  hydra -L 用户名列表.txt -p 默认密码 imap://192.168.0.1/PLAIN
  hydra -C defaults.txt -6 pop3s://[2001:db8::1]:143/TLS:DIGEST-MD5
  hydra -l admin -p 密码 ftp://[192.168.0.0/24]/
  hydra -L 登录名列表.txt -P 密码列表.txt -M 目标列表.txt ssh
```

---

参考链接

- [Hydra](https://www.kali.org/tools/hydra/)
