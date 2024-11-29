基于 Debian 的信息安全平台。

## 1 准备

kali-linux-installer-amd64.iso

```
https://www.kali.org/get-kali/
```

VMware

```
https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion
```

目录

```
C:\Users\sec\Documents\Virtual Machines\kali
```

## 2 配置

移动镜像文件到 `iso` 文件夹

```
C:\Users\sec\Documents\Virtual Machines\iso
```

VMware Workstation Pro

```
创建新的虚拟机
```

您希望使用什么类型的配置？

```
自定义
```

硬件兼容性

```
Workstation 17.5 or later
```

安装来源

```
稍后安装操作系统
```

客户机操作系统

```
Linux
```

版本

```
Debian 12.x 64 位
```

虚拟机名称

```
kali
```

位置

```
C:\Users\sec\Documents\Virtual Machines\kali
```

处理器数量

```
1
```

每个处理器的内核数量

```
2
```

此虚拟机的内存

```
4096 MB
```

网络连接

```
使用桥接网络
```

SCSI 控制器

```
LSI Logic
```

虚拟磁盘类型

```
SCSI
```

磁盘

```
创建新虚拟磁盘
```

最大磁盘大小

```
128.0 GB
```

```
将虚拟磁盘存储为单个文件
```

磁盘文件

```
C:\Users\sec\Documents\Virtual Machines\kali\kali.vmdk
```

自定义硬件

处理器

```
虚拟化引擎
虚拟化 Intel VT-x/EPT 或 AMD-V/RVI
```

CD/DVD

```
使用 ISO 映像文件
C:\Users\sec\Documents\Virtual Machines\iso\kali-linux-installer-amd64.iso
```

显示

```
3D 图形
关闭加速 3D 图形
```

拍摄快照并命名为 `配置` 

## 3 安装

开启此虚拟机进行安装

Kali Linux installer menu

```
Install
```

Select a language

```
Language:
English
```

Select your location

```
Country, territory or area:
New Zealand
```

Configure the keyboard

```
Keymap to use:
American English
```

Configure the network

```
Hostname:
kali
```

```
Domain name:
```

Set up users and passwords

```
Full name for the new user:
sec
```

```
Username for your account:
sec
```

```
Choose a password for the new user:
123456
```

```
Re-enter password to verify:
123456
```

Configure the clock

```
Select a location in your time zone:
Auckland
```

Partition disks

```
Partitioning method:
Guided - use entire disk and set up LVM
```

```
Select disk to partition:
Default
```

```
Partitioning scheme:
All files in one partition
```

```
Write the changes to disks and configure LVM?
<Yes>
```

```
Amount of volume group to use for guided partitioning:
Default
```

```
Write the changes to disks?
<Yes>
```

Software selection

```
Choose software to install:
[*] Collection of tools
[*] ... top10 -- the 10 most popular tools
[*] ... default -- recommended tools
```

Configuring grub-pc

```
Install the GRUB boot loader to your primary drive?
<Yes>
```

```
Device for boot loader installation:
/dev/
```

Finish the installation

```
Please choose <Continue> to reboot.
<Continue>
```

登录

```
kali login: sec
Password: 123456
```

设置 `root` 用户密码

```shell
┌──(sec㉿kali)-[~]
└─$ sudo passwd root
[sudo] password for sec: 123456
New password: 123456
Retype new password: 123456
passwd: password updated successfully
```

关机，拍摄快照并命名为 `安装` 

```shell
root@kali:~# init 0
```

## 4 初始化

启动虚拟机，使用 `root` 用户登录

**开启 SSH 服务** 

允许远程登录 `root` 并配置稳定连接

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/ssh/sshd_config
```

```
 33 PermitRootLogin yes
 99 ClientAliveInterval 60
100 ClientAliveCountMax 60
```

重启 SSH

```shell
┌──(root㉿kali)-[~]
└─# systemctl enable --now ssh.service && systemctl restart ssh.service
```

查看 IP

```shell
┌──(root㉿kali)-[~]
└─# ip a
```

在 Powershell 远程登录 `root` 

```powershell
PS C:\Users\sec> ssh root@[ip]
```

**修改软件源**

配置 `apt` 源

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/apt/sources.list
```

```
deb https://mirrors.ustc.edu.cn/kali kali-rolling main non-free non-free-firmware contrib

deb https://mirrors.ustc.edu.cn/debian bookworm-updates main contrib non-free non-free-firmware
```

配置优先级

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/apt/preferences
```

```
Package: *
Pin: release o=Kali,a=kali-rolling
Pin-Priority: 900

Package: *
Pin: release o=Debian,n=bookworm-updates
Pin-Priority: 800
```

获取更新

```shell
┌──(root㉿kali)-[~]
└─# apt update
```

**配置网络**

查看网络接口

```shell
┌──(root㉿kali)-[~]
└─# ip link
```

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 00:0c:29:1e:b4:76 brd ff:ff:ff:ff:ff:ff
```

配置网络接口参数

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/network/interfaces
```

```
10  # The primary network interface
11  allow-hotplug eth0
12  # iface eth0 inet dhcp
13  auto eth0
14  iface eth0 inet static
15          address [os_IP]
16          netmask 255.255.255.0
17          broadcast 192.168.1.255
18          gateway 192.168.1.1
19  # This is an autoconfigured IPv6 interface
20  # iface eth0 inet6 auto
```

修改 DNS 服务器

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/resolv.conf
```

```
nameserver 8.8.8.8
nameserver 1.1.1.1
```

在 `hosts` 文件添加域名映射

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/hosts
```

重启

```shell
┌──(root㉿kali)-[~]
└─# reboot
```

在 Powershell 删除 SSH 连接缓存

```powershell
PS C:\Users\sec> ssh-keygen -R [ip]
```

远程重新登录 `root` 

```powershell
PS C:\Users\sec> ssh root@kali.local
```

更新缓存并测试网络

```shell
┌──(root㉿kali)-[~]
└─# service networking restart && ping g.cn -c 3
```

**创建目录**

```shell
┌──(root㉿kali)-[~]
└─# mkdir -p /root/tools/driver /root/share/github /var/www/html/upload
```

关机，拍摄快照并命名为 `初始化` 

```shell
┌──(root㉿kali)-[~]
└─# init 0
```

## 5 部署

|                       实验环境                        |
| :---------------------------------------------------: |
|           [v2fly](https://github.com/v2fly)           |
|     [redsocks](https://github.com/darkk/redsocks)     |
|                 [go](https://go.dev/)                 |
|           [docker](https://www.docker.com/)           |
|           [python](https://www.python.org/)           |
|         [composer](https://getcomposer.org/)          |
| [java](https://github.com/adoptium/temurin8-binaries) |
|      [gdebi](https://github.com/linuxmint/gdebi)      |

|                           渗透测试                           |
| :----------------------------------------------------------: |
|   [antsword](https://github.com/AntSwordProject/antSword)    |
|     [arl](https://github.com/TophantTechnology/ARL-doc)      |
|         [bbscan](https://github.com/lijiejie/BBScan)         |
|       [behinder](https://github.com/rebeyond/Behinder)       |
|        [burpsuite](https://portswigger.net/burp/pro)         |
|       [cscan-go](https://github.com/ifacker/cscan-go)        |
|          [dalfox](https://github.com/hahwul/dalfox)          |
|        [dddd](https://github.com/SleepingBag945/dddd)        |
|        [dirmap](https://github.com/H4ckForJob/dirmap)        |
|   [ds_store_exp](https://github.com/lijiejie/ds_store_exp)   |
|      [ehole](https://github.com/EdgeSecurityTeam/EHole)      |
|           [exploitdb](https://www.exploit-db.com/)           |
|        [fping](https://salsa.debian.org/debian/fping)        |
|        [githack](https://github.com/lijiejie/GitHack)        |
|      [gopherus](https://github.com/tarunkant/Gopherus)       |
| [httpx-toolkit](https://gitlab.com/kalilinux/packages/httpx-toolkit) |
|     [hydra](https://github.com/vanhauser-thc/thc-hydra)      |
|   [masscan](https://github.com/robertdavidgraham/masscan)    |
|        [medusa](https://github.com/jmk-foofus/medusa)        |
|          [metasploit](https://www.metasploit.com/)           |
|            [nc](https://netcat.sourceforge.net/)             |
| [nessus](https://www.tenable.com/downloads/nessus?loginAttempted=true) |
|     [nikto](https://gitlab.com/kalilinux/packages/nikto)     |
|                  [nmap](https://nmap.org/)                   |
|       [nslookup](https://github.com/alsotang/nslookup)       |
|     [nuclei](https://github.com/projectdiscovery/nuclei)     |
|     [oneforall](https://github.com/shmilylty/OneForAll)      |
|            [rad](https://github.com/chaitin/rad)             |
|        [redsocks](https://github.com/darkk/redsocks)         |
|      [svnhack](https://github.com/callmefeifei/svnHack)      |
|          [searpy](https://github.com/j3ers3/Searpy)          |
|      [searchsploit](https://www.exploit-db.com/search)       |
|      [sqlmap](https://github.com/sqlmapproject/sqlmap)       |
|            [vscan](https://github.com/veo/vscan)             |
|    [whatweb](https://github.com/urbanadventurer/WhatWeb)     |
|          [whois](https://github.com/rfc1036/whois)           |
|        [waf-scan](https://github.com/jammny/waf-scan)        |
|     [wafw00f](https://github.com/EnableSecurity/wafw00f)     |
|    [wpscan](https://gitlab.com/kalilinux/packages/wpscan)    |
|           [xpoc](https://github.com/chaitin/xpoc)            |
|           [xray](https://github.com/chaitin/xray)            |
|                       gopher_encode.py                       |
|                     linebreak_conver.py                      |

## 6 使用

**卧底模式**

```shell
┌──(root㉿kali)-[~]
└─# kali-undercover
```

> 鼠标和触摸板
>
> Windows 10
>
> 大小：46

**历史命令**

查看历史命令

```shell
┌──(root㉿kali)-[~]
└─# history
```

**payload**

windows

```shell
┌──(root㉿kali)-[~]
└─# ls /usr/share/windows-resources/binaries/
```

**工具脚本**

```shell
┌──(root㉿kali)-[~]
└─# ls /usr/share/metasploit-framework/data/
```

挂载共享文件到 `/mnt/`

```
vmhgfs-fuse .host:/ /mnt
```

**su**

切换为 `root` 用户

```shell
┌──(sec㉿kali)-[~]
└─$ su - root
Password: 123456
┌──(root㉿kali)-[~]
└─#
```

---

参考链接

- [Kali](https://www.kali.org/)
- [Kali Docs](https://www.kali.org/docs/)
