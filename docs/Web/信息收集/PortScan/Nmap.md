一个开源的网络扫描和安全审核工具。

## 1 安装

全选安装

![全选安装](./../../../../images/Nmap/%E5%85%A8%E9%80%89%E5%AE%89%E8%A3%85.png)

安装 npcap，支持捕获和处理 Wi-Fi 网络流量

![安装 npcap，支持捕获和处理 Wi-Fi 网络流量](./../../../../images/Nmap/%E5%AE%89%E8%A3%85%20npcap%EF%BC%8C%E6%94%AF%E6%8C%81%E6%8D%95%E8%8E%B7%E5%92%8C%E5%A4%84%E7%90%86%20Wi-Fi%20%E7%BD%91%E7%BB%9C%E6%B5%81%E9%87%8F.png)

## 2 使用

运行

```powershell
PS C:\Users\sec> nmap
```

识别端口服务并检测系统

```shell
┌──(root㉿kali-23)-[~]
└─# nmap -T4 -Pn -p- -sV -O -v [host] -oX result.xml
```

绕过

```shell
┌──(root㉿kali-23)-[~]
└─# nmap -T4  -Pn -p- -sV -O -f -D RND:10 -v [host] -oX result.xml
```

使用漏洞检测脚本检测目标

```shell
┌──(root㉿Kali)-[~]
└─# nmap --script=vuln [ip] -oX result.xml
```

## 3 帮助

```shell
┌──(root㉿kali-23)-[~]
└─# nmap -h
```

```
Nmap 7.94SVN ( https://nmap.org )
用法: nmap [扫描类型] [选项] {目标说明}
目标说明:
  可以传递主机名、IP地址、网络等。
  示例: scanme.nmap.org, microsoft.com/24, 192.168.0.1; 10.0.0-255.1-254
  -iL <inputfilename>: 从主机/网络列表中输入
  -iR <num hosts>: 选择随机目标
  --exclude <host1[,host2][,host3],...>: 排除主机/网络
  --excludefile <exclude_file>: 从文件中排除列表
主机发现:
  -sL: 列出扫描目标
  -sn: Ping扫描 - 禁用端口扫描
  -Pn: 将所有主机视为在线 - 跳过主机发现
  -PS/PA/PU/PY[portlist]: 向指定端口发送TCP SYN/ACK、UDP或SCTP探测
  -PE/PP/PM: ICMP echo、timestamp和netmask请求探测
  -PO[protocol list]: IP协议Ping
  -n/-R: 从不进行DNS解析/始终解析 [默认: 有时]
  --dns-servers <serv1[,serv2],...>: 指定自定义DNS服务器
  --system-dns: 使用操作系统的DNS解析器
  --traceroute: 追踪到每个主机的跳数路径
扫描技术:
  -sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon扫描
  -sU: UDP扫描
  -sN/sF/sX: TCP Null、FIN和Xmas扫描
  --scanflags <flags>: 自定义TCP扫描标志
  -sI <zombie host[:probeport]>: 空闲扫描
  -sY/sZ: SCTP INIT/COOKIE-ECHO扫描
  -sO: IP协议扫描
  -b <FTP relay host>: FTP反弹扫描
端口指定和扫描顺序:
  -p <port ranges>: 仅扫描指定端口
    示例: -p22; -p1-65535; -p U:53,111,137,T:21-25,80,139,8080,S:9
  --exclude-ports <port ranges>: 排除指定端口的扫描
  -F: 快速模式 - 扫描比默认扫描更少的端口
  -r: 顺序扫描端口 - 不随机化
  --top-ports <number>: 扫描最常见的<number>端口
  --port-ratio <ratio>: 扫描比<ratio>更常见的端口
服务/版本检测:
  -sV: 探测开放端口以确定服务/版本信息
  --version-intensity <level>: 设置从0（轻）到9（尝试所有探测）的级别
  --version-light: 限制为最可能的探测（强度2）
  --version-all: 尝试每个单独的探测（强度9）
  --version-trace: 显示详细的版本扫描活动（用于调试）
脚本扫描:
  -sC: 等效于 --script=default
  --script=<Lua scripts>: <Lua scripts> 是逗号分隔的目录、脚本文件或脚本类别
  --script-args=<n1=v1,[n2=v2,...]>: 为脚本提供参数
  --script-args-file=filename: 在文件中提供NSE脚本参数
  --script-trace: 显示所有发送和接收的数据
  --script-updatedb: 更新脚本数据库。
  --script-help=<Lua scripts>: 显示有关脚本的帮助信息。
           <Lua scripts> 是逗号分隔的脚本文件或脚本类别。
操作系统检测:
  -O: 启用操作系统检测
  --osscan-limit: 只对可能性较高的目标执行操作系统检测
  --osscan-guess: 对所有目标执行操作系统检测
时间和性能:
  带有<time>的选项以秒为单位，或将'ms'（毫秒）、's'（秒）、'm'（分钟）或'h'（小时）附加到值上（例如 30m）。
  -T<0-5>: 设置时间模板（更高表示更快）
  --min-hostgroup/max-hostgroup <size>: 并行主机扫描组大小
  --min-parallelism/max-parallelism <numprobes>: 探测并行化
  --min-rtt-timeout/max-rtt-timeout/initial-rtt-timeout <time>: 指定探测往返时间。
  --max-retries <tries>: 限制端口扫描探测的重传次数。
  --host-timeout <time>: 在此时间后放弃目标
  --scan-delay/--max-scan-delay <time>: 调整探测间隔
  --min-rate <number>: 每秒发送不少于<number>个数据包
  --max-rate <number>: 每秒发送不超过<number>个数据包
防火墙/IDS逃避和欺骗:
  -f; --mtu <val>: 分片数据包（可选地带有给定的MTU）
  -D <decoy1,decoy2[,ME],...>: 伪装扫描
  -S <IP_Address>: 伪造源地址
  -e <iface>: 使用指定的接口
  -g/--source-port <portnum>: 使用给定的端口号
  --proxies <url1,[url2],...>: 通过HTTP/SOCKS4代理中继连接
  --data <hex string>: 向发送的数据包附加自定义负载
  --data-string <string>: 向发送的数据包附加自定义ASCII字符串
  --data-length <num>: 向发送的数据包附加随机数据
  --ip-options <options>: 使用指定的IP选项发送数据包
  --ttl <val>: 设置IP生存时间字段
  --spoof-mac <mac address/prefix/vendor name>: 伪造MAC地址
  --badsum: 发送带有虚假TCP/UDP/SCTP校验和的数据包
输出:
  -oN/-oX/-oS/-oG <file>: 将扫描输出分别输出为普通、XML、s|<rIpt kIddi3
     和Grepable格式到给定的文件名。
  -oA <basename>: 一次性以三种主要格式输出
  -v: 增加详细程度级别（使用-vv或更多以获得更大的效果）
  -d: 增加调试级别（使用-dd或更多以获得更大的效果）
  --reason: 显示端口处于特定状态的原因
  --open: 仅显示打开（或可能打开）的端口
  --packet-trace: 显示所有发送和接收的数据包
  --iflist: 打印主机接口和路由（用于调试）
  --append-output: 追加而不是覆盖指定的输出文件
  --resume <filename>: 恢复中止的扫描
  --noninteractive: 禁用键盘的运行时交互
  --stylesheet <path/URL>: 将XML输出转换为HTML的XSL样式表
  --webxml: 引用来自Nmap.Org的样式表以实现更具可移植性的XML
  --no-stylesheet: 防止将XSL样式表与XML输出关联
其他:
  -6: 启用IPv6扫描
  -A: 启用操作系统检测、版本检测、脚本扫描和跟踪路由
  --datadir <dirname>: 指定自定义Nmap数据文件位置
  --send-eth/--send-ip: 使用原始以太网帧或IP数据包发送
  --privileged: 假定用户完全具备特权
  --unprivileged: 假定用户缺少原始套接字权限
  -V: 打印版本号
  -h: 打印此帮助摘要页。
示例:
  nmap -v -A scanme.nmap.org
  nmap -v -sn 192.168.0.0/16 10.0.0.0/8
  nmap -v -iR 10000 -Pn -p 80
有关更多选项和示例，请参阅手册页（https://nmap.org/book/man.html）
```

### 3.1 端口状态解析

端口扫描是 Nmap 最基本最核心的功能，用于确定目标主机的TCP/UDP端口的开放情况。

TCO：

| 状态            | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| open            | 应用程序在该端口接收TCP连接或者UDP报文。                     |
| closed          | 关闭的端口对于nmap也是可访问的，它接收nmap探测报文并作出响应。但没有应用程序在其上监听。 |
| filtered        | 由于包过滤阻止探测报文到达端口，nmap无法确定该端口是否开放。过滤可能来自专业的防火墙设备，路由规则或者主机上的软件防火墙。 |
| unfiltered      | 未被过滤状态意味着端口可访问，但是nmap无法确定它是开放还是关闭。只有用于映射防火墙规则集的ACK扫描才会把端口分类到这个状态。 |
| open\|filtered  | 无法确定端口是开放还是被过滤，开放的端口不响应就是一个例子。没有响应也可能意味着报文过滤器丢弃了探测报文或者它引发的任何反应。UDP，IP协议,FIN,Null等扫描会引起。 |
| losed\|filtered | (关闭或者被过滤的)︰无法确定端口是关闭的还是被过滤的。       |

UDP：

| 状态           | 描述                          |
| -------------- | ----------------------------- |
| open           | 从目标端口得到任意的 UDP 应答 |
| open\|filtered | 如果目标主机没有给出应答      |
| closed         | ICMP 端口无法抵达错误         |
| filtered       | ICMP 无法抵达错误             |

### 3.2 高级使用技巧

### 3.2.1 扫描服务器：

（一般扫描 TCP 协议和 UDP 协议）

| 操作              | 描述                                                |
| ----------------- | --------------------------------------------------- |
| -O                | 显示出操作系统的类型。 每一种操作系统都有一个指纹。 |
| -f                | 以对 nmap 发送的探测数据包进行分段。                |
| -sS               | TCP 半连接扫描                                      |
| -sT               | TCP 全连接扫描                                      |
| -sU               | UDP 扫描                                            |
| -sV               | 服务版本识别                                        |
| -v                | 显示扫描的细节                                      |
| -p                | 扫描一个范围                                        |
| -p-               | 全端口扫描                                          |
| -D                | 使用诱饵扫描                                        |
| -iR               | 随机扫描（后加数字指定个数）                        |
| -Pn               | 默认主机存活，可以穿透防火墙                        |
| --randomize_hosts | 随机扫描，对目标主机的顺序随机划分（多个目标可用）  |
| --scan-delay      | 延时扫描，单位秒，调整探针之间的延迟                |
| --source-port     | 伪造端口（或者用 - g ）                             |

使用 nmap 扫描一台服务器（默认情况下，Nmap 会扫描 1000 个最有可能开放的 TCP 端口，端口共有65535个）

```shell
┌──(root㉿Kali)-[~]
└─# nmap [ip]
```

将结果导出到文件中（建议导出到 xml 文件，用于在不同系统和平台之间交换数据）

```shell
┌──(root㉿Kali)-[~]
└─# nmap [ip] > [*.xml]
```

显示扫描的细节

```shell
┌──(root㉿Kali)-[~]
└─# nmap -v [ip]
```

扫描一个端口范围 

```shell
┌──(root㉿Kali)-[~]
└─# nmap -p [port-port] [ip]
```

> 端口范围 `1 - 65535` ，`0` 号端口为空

全端口扫描

```shell
┌──(root㉿Kali)-[~]
└─# nmap -p- [ip]
```

查看此服务器开放的端口号和操作系统类型

```shell
┌──(root㉿Kali)-[~]
└─# nmap -sS -O [domain]
```

> 默认半连接扫描，加 `-sS` 也是半连接扫描
>
> `-O` 参数无法确认准确的操作系统版本时 nmap 会给出几个可能性比较高的建议

 查找指定的 `ip` 范围，开启某端口的服务器。

```shell
┌──(root㉿Kali)-[~]
└─# nmap -v -p [port] [ip/24]
```

查找多个指定的 `ip` ，开启 `80` 端口的服务器。

```shell
┌──(root㉿Kali)-[~]
└─# nmap -v -p 80 [ip] [ip]
```

扫描 `*.txt`

```shell
┌──(root㉿Kali)-[~]
└─# nmap -iL host.txt 
```

更隐蔽的去扫描（频繁扫描会被屏蔽或者锁定 IP 地址）。

| 操作              | 描述                                               |
| ----------------- | -------------------------------------------------- |
| --randomize_hosts | 随机扫描，对目标主机的顺序随机划分（多个目标可用） |
| --scan-delay      | 延时扫描，单位秒，调整探针之间的延迟               |

随机扫描：

```shell
┌──(root㉿Kali)-[~]
└─#  nmap -v --randomize-hosts -p [port] [ip/24]
```

随机扫描+延时扫描 ，默认单位秒

```shell
┌──(root㉿Kali)-[~]
└─# nmap -v --randomize-hosts --scan-delay 3000ms -p [port] [ip/24]
```

### 3.2.1.1 使用通配符指定 `ip` 地址

```shell
┌──(root㉿Kali)-[~]
└─# nmap -v --randomize-hosts --scan-delay 30 -p [port] 192.*.1.3-8
```

扫网段内的所有 `ip`

```shell
┌──(root㉿Kali)-[~]
└─# nmap 192.168.1.*
```

> 共 `254` 个 `ip`

扫 192.168.1 内的所有 `ip`

```shell
┌──(root㉿Kali)-[~]
└─#  nmap 192.168.*.*		
```

> `254 x 254` 个 `ip`

扫描全球 `ip`

```shell
┌──(root㉿Kali)-[~]
└─# nmap *.*.*.* 
```

`TCP Connect`  全连接扫描

```shell
┌──(root㉿Kali)-[~]
└─# nmap -sT [ip]
```

`UDP` 扫描

```shell
┌──(root㉿Kali)-[~]
└─#  nmap -sU [ip]
```

报文分段扫描

```shell
┌──(root㉿Kali)-[~]
└─# nmap -f -v [ip]
```

> `-f` 对 nmap 发送的探测数据包进行分段。这样将原来的数据包分成几个部分以绕过目标网络的防御机制

### 3.2.1.2 隐蔽 IP 和端口进行扫描

> 在初始的 ping 扫描（ICMP、SYN、ACK 等)阶段或真正的端口扫描，以及远程操作系统检测（-
> O)阶段都可以使用诱饵主机选项。但是在进行版本检测或 TCP 连接扫描时，诱饵主机选项是无效的

随机 `3` 个诱饵

```shell
┌──(root㉿Kali)-[~]
└─# nmap -D RND:3 [ip]
```

使用自己 `ip` 作为诱饵

```shell
┌──(root㉿Kali)-[~]
└─# nmap -D ME [ip]
```

指定单个 IP 192.168.1.6 作为诱饵

```shell
┌──(root㉿Kali)-[~]
└─# nmap -D [ip] [ip]
```

指定多个 `ip` 作为诱饵对 `ip`进行探测

```shell
┌──(root㉿Kali)-[~]
└─#  nmap -D [ip],[ip] [ip]
```

伪造源 `port` 对目标进行扫描

```shell
┌──(root㉿Kali)-[~]
└─# nmap --source-port [port] [ip]
```

或者

```shell
┌──(root㉿Kali)-[~]
└─# nmap -g [port] [ip]
```

从互联网上随机选择 `10` 台主机扫描是否开放某 `port`

```shell
┌──(root㉿Kali)-[~]
└─# nmap -v -iR 10 -p [port]
```

将所有主机视为联机，跳过主机发现

```shell
┌──(root㉿Kali)-[~]
└─# nmap -Pn [ip]
```

> 这种方式可以穿透防火墙，避免被防火墙发现

### 3.3 脚本介绍

Intense scan 

> (nmap -T4 -A -v) 
> 一般来说，Intense scan 可以满足一般扫描 
> -T4 加快执行速度 
> -A 操作系统及版本探测 
> -v 显示详细的输出 

Intense scan plus UDP 

> (nmap -sS -sU -T4 -A -v) 
> 即 UDP 扫描 
> -sS TCP SYN 扫描 
> -sU UDP 扫描 

Intense scan,all TCP ports 

> (nmap -p 1-65536 -T4 -A -v) 
> 扫描所有 TCP 端口，范围在 1-65535，试图扫描所有端口的开放情况，速度比较慢。 
> -p 指定端口扫描范围 

Intense scan,no ping 

> (nmap -T4 -A -v -Pn) 
> 非 ping 扫描 
> -Pn 非 ping 扫描 

Ping scan 

> (nmap -sn) 
> Ping 扫描 
> 优点：速度快。 
> 缺点：容易被防火墙屏蔽，导致无扫描结果 
> -sn ping 扫描 

Quick scan 

> (nmap -T4 -F) 
> 快速的扫描 
> -F 快速模式。 

Quick scan plus 

> (nmap -sV -T4 -O -F --version-light) 
> 快速扫描加强模式 
> -sV 探测端口及版本服务信息。 
> -O 开启 OS 检测 
> --version-light 设定侦测等级为 2。 

Quick traceroute 

> (nmap -sn --traceroute) 
> 路由跟踪 
> -sn Ping 扫描，关闭端口扫描 
> -traceroute 显示本机到目标的路由跃点。 

Regular scan 

> 常规扫描 

Slow comprehensive scan 

> (nmap -sS -sU -T4 -A -v -PE -PP -PS80,443,-PA3389,-PU40125 -PY -g 53 --script all) 
> 慢速全面扫描。

### 3.3.1 脚本使用

| 操作      | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| auth      | 负责处理鉴权证书（绕开鉴权）的脚本                           |
| broadcast | 在局域网内探查更多服务开启状况，如 dhcp/dns/sqlserver 等服务 |
| brute     | 提供暴力破解方式，针对常见的应用如 http/snmp 等              |
| default   | 使用-sC 或-A 选项扫描时候默认的脚本，提供基本脚本扫描能力    |
| discovery | 对网络进行更多的信息，如 SMB 枚举、SNMP 查询等               |
| dos       | 用于进行拒绝服务攻击                                         |
| exploit   | 利用已知的漏洞入侵系统                                       |
| external  | 利用第三方的数据库或资源 如进行 whois 解析                   |
| fuzzer    | 模糊测试的脚本，发送异常的包到目标机，探测出潜在漏洞 intrusive: 入侵性的脚本，此类脚本可能引发对方的 IDS/IPS 的记录或屏蔽 |
| malware   | 探测目标机是否感染了病毒、开启了后门等信息                   |
| safe      | 此类与 intrusive 相反，属于安全性脚本                        |
| version   | 负责增强服务与版本扫描（Version Detection）功能的脚本        |
| vuln      | 负责检查目标机是否有常见的漏洞（Vulnerability），如是否有 MS08_067 |

Nmap 内置了许多脚本，都存放在以下目录中。

```shell
┌──(root㉿Kali)-[~]
└─# ls /usr/share/nmap/scripts
```

使用所有的漏洞检测脚本检测目标

```shell
┌──(root㉿Kali)-[~]
└─# nmap --script=vuln [ip]
```

查看漏洞相关脚本

```shell
┌──(root㉿Kali-24)-[/usr/share/nmap/scripts]
└─# ls *vuln*
```

指定脚本扫描

```shell
┌──(root㉿Kali-24)-[/usr/share/nmap/scripts]
└─# nmap --script=smb-vuln-ms06-025.nse [ip]
```

---

参考链接

- [Nmap](https://nmap.org/)
- [Nmap 参考指南](https://nmap.org/man/zh/)
