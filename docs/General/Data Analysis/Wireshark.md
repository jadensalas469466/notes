## 1 安装

选择安装全部 extcap

![选择安装全部 extcap](./../../../images/Wireshark/%E9%80%89%E6%8B%A9%E5%AE%89%E8%A3%85%E5%85%A8%E9%83%A8%20extcap.png)

关联文件

![关联文件](./../../../images/Wireshark/%E5%85%B3%E8%81%94%E6%96%87%E4%BB%B6.png)

安装 Npcap

![安装 Npcap](./../../../images/Wireshark/%E5%AE%89%E8%A3%85%20Npcap.png)

安装 USBPcap

![安装 USBPcap](./../../../images/Wireshark/%E5%AE%89%E8%A3%85%20USBPcap.png)

Npcap 支持捕获和处理 Wi-Fi 网络流量

![Npcap 支持捕获和处理 Wi-Fi 网络流量](./../../../images/Wireshark/Npcap%20%E6%94%AF%E6%8C%81%E6%8D%95%E8%8E%B7%E5%92%8C%E5%A4%84%E7%90%86%20Wi-Fi%20%E7%BD%91%E7%BB%9C%E6%B5%81%E9%87%8F.png)

USBPcap 完整安装

![USBPcap 完整安装](./../../../images/Wireshark/USBPcap%20%E5%AE%8C%E6%95%B4%E5%AE%89%E8%A3%85.png)

重启

![重启](./../../../images/Wireshark/%E9%87%8D%E5%90%AF.png)

## 2 初始化

字体大小修改为 18

![字体大小修改为 18](./../../../images/Wireshark/%E5%AD%97%E4%BD%93%E5%A4%A7%E5%B0%8F%E4%BF%AE%E6%94%B9%E4%B8%BA%2018.png)

## 3 使用

wireshark 是一种常用的网络协议分析工具，它可以对网络中的通信数据包进行捕获、解析、分析和展示。

| 功能                             |
| -------------------------------- |
| 了解网络特征                     |
| 查看网络上的通信主体             |
| 确认谁或是哪些应用在占用网络带宽 |
| 识别网络使用高峰时间             |
| 识别可能的攻击或恶意活动         |
| 寻找不安全以及滥用网络资源的应用 |

| 快速分析数据包技巧                                           |
| ------------------------------------------------------------ |
| 确定 Wireshark 的物理位置。如果没有一个正确的位置，启动 Wireshark 后会花费很长的时间捕获一些与自己无关的数据。 |
| 选择捕获接口。一般都是选择连接到 Internet 网络的接口，这样才可以捕获到与网络相关的数据。否则，捕获到的其它数据对自己也没有任何帮助。 |
| 使用捕获过滤器。通过设置捕获过滤器，可以避免产生过大的捕获数据。这样用户在分析数据时，也不会受其它数据干扰。而且，还可以为用户节约大量的时间。 |
| 使用显示过滤器。通常使用捕获过滤器过滤后的数据，往往还是很复杂。为了使过滤的数据包再更细致，此时使用显示过滤器进行过滤。 |
| 使用着色规则。通常使用显示过滤器过滤后的数据，都是有用的数据包。如果想更加突出的显示某个会话，可以使用着色规则高亮显示。 |
| 构建图表。如果用户想要更明显的看出一个网络中数据的变化情况，使用图表的形式可以很方便的展现数据分布情况。 |
| 重组数据。当传输较大的图片或文件时，需要将信息分布在多个数据包中。这时候就需要使用重组数据的方法来抓取完整的数据。Wireshark 的重组功能，可以重组一个会话中不同数据包的信息，或者是重组一个完整的图片或文件。 |

## 4 抓包

`可通过抓包分析系统被植入的后门`

启动 wireshark

![WireShark (1)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(1).png)

选择有流量的网卡（在物理机中要用物理机网卡，any表示所有）

![WireShark (2)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(2).png)

### 4.1 捕获过滤

只抓取符合条件的数据包

`注意：筛选条件使用小写，大写不识别。`

| 操作       | 描述                               |
| ---------- | ---------------------------------- |
| host       | 添加 IP，抓取所有流经主机的数据包  |
| ether host | 添加 MAC，抓取所有流经主机的数据包 |
| src host   | 添加 IP，只抓取主机发送的数据包    |
| dst host   | 添加 IP，只抓取主机接收的数据包    |
| port       | 添加端口号，只抓取该端口的数据包   |
| tcp        | 只抓取该协议的数据包               |
| udp        | 只抓取该协议的数据包               |
| arp        | 只抓取该协议的数据包               |
| icmp       | 只抓取该协议的数据包               |
| udp        | 只抓取该协议的数据包               |
| dns        | 只抓取该协议的数据包               |
| http       | 只抓取该协议的数据包               |

oicq 以及 dns 都是基于 udp 的传输层之上的协议

`客户端向 DNS 服务器查询域名，一般返回的内容都不超过 512 字节，用 UDP 传输即可。不用经过三次握手，这样 DNS 服务器负载更低，响应更快。理论上说，客户端也可以指定向 DNS 服务器查询时用 TCP，但事实上，很多 DNS 服务器进行配置的时候，仅支持 UDP 查询包。`

点开选项

![WireShark (3)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(3).png)

添加规则

![WireShark (4)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(4).png)

捕获流经 192.168.1.5 的数据包

![WireShark (5)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(5).png)

点击开始之后就会自动进行抓包

`访问完成后点击停止抓包即可。`

### 4.2 显示过滤

显示符合条件的数据包，但依然捕获

![WireShark (6)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(6).png)

筛选源地址是 192.168.1.5 并且目的地址是 192.168.1.1

`src host 192.168.1.5 表示源 IP 地址
dst host 192.168.1.1 表示目的地址`

ip.src_host == 192.168.1.5 and ip.dst_host == 192.168.1.1

`or 表示满足左右其中一个条件就会显示符合条件的数据包，and 表示左右 2 个条件都满足才会显示。`

![WireShark (7)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(7).png)

筛选192.168.1.5 和192.168.1.1 互相通信的数据包

`ip.addr == 192.168.1.5 表示 IPv4 地址，&& 用法与 and 相同，|| 与 or 相同`

ip.addr == 192.168.1.5 && ip.addr == 192.168.1.1

![WireShark (8)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(8).png)

或者结合 () 使用

`(ip.src_host == 192.168.1.5 and ip.dst_host == 192.168.1.1) or (ip.src_host == 192.168.1.1 and ip.addr == 192.168.1.5)` 

混杂模式概述：

`混杂模式就是接收所有经过网卡的数据包，包括不是发给本机的包，即不验证MAC 地址。`

`普通模式下只接收网卡发给本机的包（包括广播包）传递给上层程序，其它的包一律丢弃。`

`一般来说，混杂模式不会影响网卡的正常工作，多在网络监听工具上使用。`
关闭和开启混杂模式方法：

`关闭和开启混杂模式前，需要停止当前抓包。`

![WireShark (9)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(9).png)

`默认就是开启混杂模式。`

## 5 流量分析

通过指纹特征识别程序

`HTTP 协议是明文，可以通过 http.request.method == POST 语法捕获`

`协议分析的时候我们关闭混淆模式，避免一些干扰的数据包存在。`

### 5.1 显示

可在视图中选择显示样式

![WireShark (10)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(10).png)

在列头部上右键修改

![WireShark (11)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(11).png)

可在编辑→首选项中根据需要增改规则

![WireShark (12)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(12).png)

### 5.2 统计

### 5.2.1 协议分级

![WireShark (13)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(13).png)

可排序

![WireShark (14)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(14).png)

### 5.2.2 会话

![WireShark (15)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(15).png)

重点看 IPv4

![WireShark (16)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(16).png)

可通过传输对象过滤

![WireShark (17)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(17).png)

### 5.2.3 端点

![WireShark (18)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(18).png)

分组长度（按照数据包大小排序）

![WireShark (19)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(19).png)

### 5.2.4 追踪流

右键追踪（从起点追踪）

![WireShark (20)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(20).png)

### 5.3 ARP 协议

`可以通过 # nmap -sn 192.168.1.1 产生一个 ARP 协议数据包`

地址解析协议是一个通过解析网络层地址来找寻数据链路层地址的网络传输协议，它在 IPv4 中极其重要。ARP 是通过网络地址来定位 MAC 地址。

![WireShark (21)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(21).png)

info

Who has 192.168.1.5? Tell 192.168.1.1 

`谁有 192.168.1.5 的 MAC ？告诉 192.168.1.1`

查看 Address Resolution Protocol (request) ARP 请求包内容：

![WireShark (22)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(22).png)

| 名称                                                         | 描述                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| Address Resolution Protocol (request)                        | ARP 地址解析协议 request 表示请求包                    |
| Hardware type: Ethernet (1)                                  | 硬件类型                                               |
| Protocol type: IPv4 ( 0x0800 )                               | 协议类型                                               |
| Hardware size: 6                                             | 硬件地址长度                                           |
| Protocol size: 4                                             | 协议长度                                               |
| Opcode:_ request ( 1 )                                       | 操作码，该值为 1 表示 ARP 请求包，为 2 表示 ARP 回复包 |
| Sender MAC address: VMware_f1:35:ee (00:0c:29:f1:35:ee)      | 源 MAC 地址                                            |
| Sender IP address: 192.168.1.1                               | 源 IP 地址                                             |
| Target MAC address: 00:00:00_ 00: 00:00 (00: 00: 00 :00: 00:00) | 目标 MAC 地址                                          |
| Target IP address: 192.168.1.5                               | 目标 IP 地址                                           |

### 5.4 ICMP 协议

`可以通过 # ping 192.168.1.1 产生一个 ICMP 协议数据包`

把之前的数据包清空掉

![WireShark (23)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(23).png)

筛选 ICMP 协议的数据包

![WireShark (24)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(24).png)

`可以看到这是个 4 层的协议包`

请求包

![WireShark (25)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(25).png)

应答包

![WireShark (26)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(26).png)

工作过程：

> 本机发送一个 ICMP Echo Request 的包
> 接收方返回一个 ICMP Echo Reply，包含了接受到数据拷贝和一些其他指令

### 5.5 TCP 协议

`可以通过 Xshell 远程连接 Kali Linux 产生一个 TCP 协议数据包`

![WireShark (27)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(27).png)

 SYN 数据包

![WireShark (28)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(28).png)

打开标志位的详细信息

![WireShark (29)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(29).png)

`这是一个 SYN 数据包，SYN=1 表示发送一个链接请求。这时 Seq 和 ACK 都是 0 。`

第二个数据包

![WireShark (30)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(30).png)

Flags 位信息

![WireShark (31)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(31).png)

`服务端收到 SYN 连接请求返回的数据包 SYN=1,ACK=1 表示回应第一个 SYN 数据包。`

看第三个数据包

![WireShark (32)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(32).png)

`到这里三次握手过程就结束了。`

生成一个图表来观察数据交互的过程

![WireShark (33)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(33).png)

限制显示过滤器：使用显示过滤规则

流类型：选择链接类型

![WireShark (34)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(34).png)

三次握手，四次挥手

![WireShark (35)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(35).png)

![WireShark (36)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(36).png)

第一次挥手：

`服务端发送一个 [FIN+ACK] ，表示自己没有数据要发送了，想断开连接，并进入 FIN_WAIT_1 状态。`

第二次挥手：

`客户端收到 FIN 后，知道不会再有数据从服务端传来，发送 ACK 进行确认，确认序号`
`为收到序号+1（与 SYN 相同，一个 FIN 占用一个序号），客户端进入 CLOSE_WAIT 状态。`

第三次挥手：

`客户端发送 [FIN+ACK] 给对方，表示自己没有数据要发送了，客户端进入 LAST_ACK 状态，然后直接断开 TCP 会话的连接，释放相应的资源。`

第四次挥手：

`服务户端收到了客户端的 FIN 信令后，进入 TIMED_WAIT 状态，并发送 ACK 确认消息。服务端在 TIMED_WAIT 状态下，等待一段时间，没有数据到来，就认为对面已经收到了自己发送的 ACK 并正确关闭了进入 CLOSE 状态，自己也断开了 TCP 连接，释放所有资源。当客户端收到服务端的 ACK 回应后，会进入 CLOSE 状态并关闭本端的会话接口，释放相应资源。`

### 5.6 HTTP 协议

`可以通过 # curl -I baidu.com 产生一个 TCP 协议数据包（curl 是一个在命令行下工作的文件传输工具，我们这里用来发送 http 请求 -I 表示仅返回头部信息）。`

HTTP 是 TCP 的上层协议，所以 TCP 的数据会包含 HTTP 协议的数据包

![WireShark (37)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(37).png)

`第 4 个和第 6 个是我们的 HTTP 数据包。`

第一步：

`我们我们发送了一个 HTTP 的 HEAD 请求`

第二步：

`服务器收到我们的请求返回了一个 Seq/ACK 进行确认`

第三步：

`服务器将 HTTP 的头部信息返回给我们客户端 状态码为 200 表示页面正常`

第四步：

`客户端收到服务器返回的头部信息向服务器发送 Seq/ACK 进行确认`
`发送完成之后客户端就会发送 FIN/ACK 来进行关闭链接的请求`

可右键追踪流

![WireShark (38)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(38).png)

![WireShark (39)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(39).png)

## 6 解决服务器被黑上不了网

`场景：服务器被黑上不了网，可以 ping 通网关，但是不能上网。`

### 6.1 模拟场景

修改主机 TTL 值为 1

```
┌──(root㉿Kali)-[~]
└─# echo "1" > /proc/sys/net/ipv4/ip_default_ttl
```

`TTL ： 数据报文的生存周期。
linux 操作系统默认值：64，每经过一个路由节点，TTL 值减 1。TTL 值为 0 时，说明目标地址不可达并返回：Time to live exceeded
作用： 防止数据包，无限制在公网中转发`

尝试 ping 网关

```
┌──(root㉿Kali)-[~]
└─# ping 192.168.1.1 -c 1
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=0.846 ms

--- 192.168.1.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.846/0.846/0.846/0.000 ms
```

`成功`

尝试 ping 外网

```
┌──(root㉿Kali)-[~]
└─# ping qq.com -c 1
PING qq.com (111.30.144.71) 56(84) bytes of data.
From 192.168.1.1 (192.168.1.1) icmp_seq=1 Time to live exceeded		“超过生存时间”

--- qq.com ping statistics ---
1 packets transmitted, 0 received, +1 errors, 100% packet loss, time 0ms
```

使用 Wireshark 筛选 ICMP 协议

![WireShark (40)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(40).png)

` 第一个包是发送了一个 ping 请求包 ttl=1
然后收到了 192.168.1.1 返回给我们的数据包告诉我们超过数据包生存时间，数据包被丢弃`

把 TTL 值修改成 2

```
┌──(root㉿Kali)-[~]
└─# echo "2" > /proc/sys/net/ipv4/ip_default_ttl
```

![WireShark (41)](./../../../images/Wireshark/%E4%BD%BF%E7%94%A8/WireShark%20(41).png)

`返回我们数据包被丢弃的源地址变成了 100.0.208.1 ，这证明了数据包在网络中已经到达了下一个网络设备才被丢弃，由此我们还判断出我们的运营商网关地址为 100.0.208.1 ，但是我们并没有到达目标主机。`

恢复系统内核参数

```
┌──(root㉿Kali)-[~]
└─# echo "64" > /proc/sys/net/ipv4/ip_default_ttl
```

尝试 ping 外网

```
┌──(root㉿Kali)-[~]
└─# ping qq.com -c 1                             
PING qq.com (111.30.144.71) 56(84) bytes of data.
64 bytes from 111.30.144.71 (111.30.144.71): icmp_seq=1 ttl=55 time=13.1 ms

--- qq.com ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 13.114/13.114/13.114/0.000 ms
```

`目标返回给我们的 TTL 值为 55，这表示我们的 TTL 值需要大于 64-55=9 才可以访 qq.com`

---

Refrences

- [Wireshark](https://www.wireshark.org/)
