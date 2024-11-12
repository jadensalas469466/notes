## 准备

debian-amd64-DVD-1.iso

```
https://www.debian.org/distrib/
```

VMware

```
https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion
```

目录

```
C:\Users\sec\Documents\virtual machines\debian
```

## 配置

移动镜像文件到 `iso` 文件夹

```
C:\Users\sec\Documents\virtual machines\iso
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
debian
```

位置

```
C:\Users\sec\Documents\virtual machines\debian
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
C:\Users\sec\Documents\virtual machines\debian\debian.vmdk
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
C:\Users\sec\Documents\virtual machines\iso\debian-amd64-DVD-1.iso
```

显示

```
3D 图形
关闭加速 3D 图形
```

拍摄快照并命名为 `配置` 

## 安装

开启此虚拟机进行安装

Debian GNU/Linux installer menu

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
debian
```

```
Domain name:
```

Set up users and passwords

```
Root password:
123456
```

```
Re-enter password to verify:
123456
```

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

Configure the package manager

```
Scan extra installation media?
<No>
```

```
Use a network mirror?
<No>
```

Configuring popularity- contest

```
Participate in the package usage survey
<No>
```

Software selection

```
Choose software to install:
[*] SSH server
[*] standard system utilities
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
debian login: root
Password: 123456
```

关机，拍摄快照并命名为 `安装` 

```shell
root@debian:~# init 0
```

## 初始化

启动虚拟机，使用 `root` 用户登录

**开启 SSH 服务**

允许远程登录 `root` 并配置稳定连接

```shell
root@debian:~# nano /etc/ssh/sshd_config
```

```
 33 PermitRootLogin yes
 99 ClientAliveInterval 60
100 ClientAliveCountMax 60
```

重启 SSH

```shell
root@debian:~# systemctl enable --now ssh.service && systemctl restart ssh.service
```

查看 IP

```shell
root@debian:~# ip addr
```

在 Powershell 远程登录 `root` 

```powershell
PS C:\Users\sec> ssh root@[ip]
```

**修改软件源**

配置 `apt` 源

```shell
root@debian:~# nano /etc/apt/sources.list
```

```
deb http://mirrors.ustc.edu.cn/debian bookworm-updates main contrib non-free non-free-firmware
deb-src http://mirrors.ustc.edu.cn/debian bookworm-updates main contrib non-free non-free-firmware

deb http://mirrors.ustc.edu.cn/debian bookworm main contrib non-free non-free-firmware
deb-src http://mirrors.ustc.edu.cn/debian bookworm main contrib non-free non-free-firmware
```

配置优先级

```shell
root@debian:~# nano /etc/apt/preferences
```

```
Package: *
Pin: release o=Debian,n=bookworm
Pin-Priority: 700

Package: *
Pin: release o=Debian,n=bookworm-updates
Pin-Priority: 800
```

获取更新

```shell
root@debian:~# apt update
```

安装基础工具

```shell
root@debian:~# apt install -y curl vim net-tools build-essential dkms linux-headers-$(uname -r)
```

**配置网络**

查看网络接口

```shell
root@debian:~# ip link
```

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 00:0c:29:3e:6a:ac brd ff:ff:ff:ff:ff:ff
    altname enp2s1
```

配置网络接口参数

```shell
root@debian:~# vim /etc/network/interfaces
```

```
10  # The primary network interface
11  allow-hotplug ens33
12  # iface ens33 inet dhcp
13  auto ens33
14  iface ens33 inet static
15          address「os_IP」
16          netmask 255.255.255.0
17          broadcast 192.168.1.255
18          gateway 192.168.1.1
19  # This is an autoconfigured IPv6 interface
20  # iface ens33 inet6 auto
```

修改 DNS 服务器

```shell
root@debian:~# vim /etc/resolv.conf
```

```
nameserver 8.8.8.8
nameserver 1.1.1.1
```

在 `hosts` 文件添加域名映射

```shell
root@debian:~# vim /etc/hosts
```

重启

```shell
root@debian:~# reboot
```

在 Powershell 中删除 SSH 连接缓存

```powershell
PS C:\Users\sec> ssh-keygen -R [ip]
```

远程重新登录 `root` 

```powershell
PS C:\Users\sec> ssh root@debian.local
```

更新缓存并测试网络

```shell
root@debian:~# service networking restart && ping g.cn -c 3
```

**创建目录**

```shell
root@debian:~# mkdir -p /root/tool/script /root/tool/driver /var/www/html/upload
```

关机，拍摄快照并命名为 `初始化` 

```shell
root@debian:~# init 0
```

## 部署

|                      服务器                      |
| :----------------------------------------------: |
|        [UFW](https://github.com/jbq/ufw)         |
|        [Caddy](https://caddyserver.com/)         |
|         [V2Ray](https://www.v2fly.org/)          |
| [fail2ban](https://github.com/fail2ban/fail2ban) |
|        [Tor](https://www.torproject.org/)        |
|         [SolusVM](https://solusvm.com/)          |
|       [Syncthing](https://syncthing.net/)        |
|  [bind9](https://github.com/isc-projects/bind9)  |

|                           虚拟机                            |
| :---------------------------------------------------------: |
|                 [git](https://git-scm.com/)                 |
|              [v2fly](https://github.com/v2fly)              |
|  [proxychains4](https://github.com/rofl0r/proxychains-ng)   |
|             [python3](https://www.python.org/)              |
|                    [go](https://go.dev/)                    |
|                [java](https://adoptium.net/)                |
|           [apache2](https://www.apache.org/free/)           |
|                 [php](https://www.php.net/)                 |
|            [composer](https://getcomposer.org/)             |
|           [mysql](https://www.mongodb.com/zh-cn)            |
|              [docker](https://www.docker.com/)              |
| [pikachu](https://github.com/zhuifengshaonianhanlu/pikachu) |
|          [dvwa](https://github.com/digininja/DVWA)          |

## 使用

### 网络配置

禁用 `NetworkManager` 

```shell
root@debian:~# systemctl disable --now NetworkManager
```

配置网络接口参数

```shell
root@debian:~# vim /etc/network/interfaces
```

```
 7  auto lo
 8  iface lo inet loopback
 9  #iface eth0 inet dhcp	# 禁用 dhcp
10  auto eth0				# 激活 eth0
11  iface eth0 inet static	# 声明静态网络
12  address 192.168.1.17	# 配置静态 ip
13  netmask 255.255.255.0	# 配置子网掩码
14  gateway 192.168.1.1		# 配置网关
```

> 一个系统只能配置一个网关

修改 `dns` 服务器

```shell
root@debian:~# vim /etc/resolv.conf
```

```
# Generated by NetworkManager
nameserver 8.8.8.8
nameserver 1.1.1.1
```

重启网络服务

```shell
root@debian:~# systemctl restart networking && systemctl restart networking
```

修改 `hosts` 文件添加域名映射

```shell
root@debian:~# vim /etc/hosts
```

```
192.168.1.13	win.local
192.168.1.14	kali.local
192.168.1.15	purple.local
```

### 配置无线网卡驱动

查看内核版本

```shell
┌──(root㉿kali)-[~]
└─# uname -r
6.5.0-kali3-amd64
```

安装对应的版本

> http://http.kali.org/kali/pool/main/l/linux/

```shell
┌──(root㉿kali)-[~]
└─# wget http://http.kali.org/kali/pool/main/l/linux/linux-compiler-gcc-13-x86_6.5.13-1kali2_amd64.deb && dpkg -i linux-compiler-gcc-13-x86_6.5.13-1kali2_amd64.deb && rm -rf linux-compiler-gcc-13-x86_6.5.13-1kali2_amd64.deb
```

安装依赖

```shell
┌──(root㉿kali)-[~]
└─# apt install -y build-essential dkms
```

下载驱动

```shell
┌──(root㉿kali)-[~]
└─# git clone https://github.com/aircrack-ng/rtl8812au.git /root/tools/drivers/rtl8812au
```

安装驱动

```shell
┌──(root㉿kali)-[~]
└─# cd /root/tools/drivers/rtl8812au && make dkms_install && cd
```

> 卸载
>
> ```shell
> ┌──(root㉿kali)-[~]
> └─# cd /root/tools/drivers/rtl8812au && make dkms_remove && cd
> ```

### 更新

获取更新

```shell
┌──(root㉿kali)-[~]
└─# apt update
```

完全升级

```shell
┌──(root㉿kali)-[~]
└─# apt full-upgrade -y
```

> 需要重启

清理缓存

```shell
┌──(root㉿kali)-[~]
└─# apt clean
```

### 配置 rdp 远程桌面

> 仅服务器

安装 xrdp

```shell
┌──(root㉿kali)-[~]
└─# apt install -y xrdp
```

配置开机自启

```shell
┌──(root㉿kali)-[~]
└─# systemctl enable --now xrdp
```

> 每个账户只允许有一处登录

### 配置密钥连接 ssh

> 仅服务器

生成密钥，将公钥内容添加到目标服务器

```shell
┌──(root㉿kali)-[~]
└─# vim ~/.ssh/authorized_keys
```

禁止密码验证连接

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/ssh/sshd_config
```

```
57	#PasswordAuthentication yes
57	PasswordAuthentication no
```

重启服务

```shell
┌──(root㉿kali)-[~]
└─# systemctl restart ssh
```

### 系统信息

查看 CPU 使用情况

```
top
```

查看详细的 CPU 信息

```
lscpu
```

查看内存使用情况

```
free -h
```

查看磁盘使用情况

```
df -h
```

查看详细的磁盘信息

```
lsblk
```

列出已安装的与SSH相关的软件包

```
dpkg -l | grep ssh
```

### 挂载共享文件

打开配置文件配置别名

```shell
┌──(root㉿purple)-[~]
└─# vim ~/.zshrc
```

```
   243  # some more ls aliases
   244  alias ll='ls -l'
   245  alias la='ls -A'
   246  alias l='ls -CF'
   247  alias share='vmhgfs-fuse .host:/ /mnt'
```

使配置生效

```shell
┌──(root㉿purple)-[~]
└─# source ~/.zshrc
```

---

参考链接

- [debian](https://www.debian.org/)

