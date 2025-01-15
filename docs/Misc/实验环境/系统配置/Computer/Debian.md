一个稳定的服务器操作系统.

## 1. 准备

debian-12.8.0-amd64-DVD-1.iso

```
https://www.debian.org/distrib/
```

VMware

```
https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion
```

目录

```
C:\Users\sec\Documents\Virtual Machines\debian
```

## 2. 配置

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
debian
```

位置

```
C:\Users\sec\Documents\Virtual Machines\debian
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
64.0 GB
```

```
将虚拟磁盘存储为单个文件
```

磁盘文件

```
C:\Users\sec\Documents\Virtual Machines\debian\debian.vmdk
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
C:\Users\sec\Documents\Virtual Machines\iso\debian-12.8.0-amd64-DVD-1.iso
```

拍摄快照并命名为 `配置` 

## 3. Install

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
United States
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
Eastern
```

Partition disks

```
Partitioning method:
Guided - use entire disk
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
Select a partitions to modify its settings
Finish partitioning and write changes to disk
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
Participate in the package usage survey?
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

查看 IP

```
┌──(root@debian)-[~]
└─# ip a
```

关机，拍摄快照并命名为 `安装` 

```
┌──(root@debian)-[~]
└─# init 0
```

## 4. 初始化

启动虚拟机，使用 SSH 登录 `sec` 用户

```
PS C:\Users\sec> ssh sec@<os-ip>
```

切换到 `root` 用户

```
┌──(sec@debian)-[~]
└─$ su - root
```

配置 `apt` 源

```
┌──(root@debian)-[~]
└─# nano /etc/apt/sources.list
```

```
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-backports main contrib non-free non-free-firmware
deb https://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
```

更新系统

```
┌──(root@debian)-[~]
└─# apt update && apt full-upgrade \
&& apt clean && apt autoremove --purge
```

安装常用工具

```
┌──(root@debian)-[~]
└─# apt install -y vim curl sudo tree unzip apache2 build-essential libpcap-dev \
zsh zsh-syntax-highlighting zsh-autosuggestions \
&& systemctl enable --now apache2.service \
&& chsh -s $(which zsh)
```

允许远程登录 `root` 并配置稳定连接

```
┌──(root@debian)-[~]
└─# vim /etc/ssh/sshd_config
```

```
 33 PermitRootLogin yes
 99 ClientAliveInterval 60
100 ClientAliveCountMax 60
```

重启 SSH

```
┌──(root@debian)-[~]
└─# systemctl restart ssh.service
```

配置网络接口参数

```
┌──(root@debian)-[~]
└─# vim /etc/network/interfaces
```

```
10  # The primary network interface
11  allow-hotplug ens33
12  # iface ens33 inet dhcp
auto ens33
iface ens33 inet static
    address 192.168.1.203
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
19  # This is an autoconfigured IPv6 interface
20  # iface ens33 inet6 auto
```

配置 DNS 服务器

```
┌──(root@debian)-[~]
└─# nano /etc/resolv.conf
```

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

在 `hosts` 文件添加域名映射

```
┌──(root@debian)-[~]
└─# vim /etc/hosts
```

重启

```
┌──(root@debian)-[~]
└─# reboot
```

在 Powershell 中删除 SSH 连接缓存

```
PS C:\Users\sec> ssh-keygen -R <os-ip>
```

等待虚拟机启动, 使用 SSH 登录 `root` 用户

```
PS C:\Users\sec> ssh root@debian
```

测试网络

```
┌──(root@debian)-[~]
└─# ping g.cn -c 3
```

配置 Zsh

```
┌──(root@debian)-[~]
└─# curl -LO https://raw.githubusercontent.com/jadensalas469466/config/refs/heads/main/Zsh/.zshrc \
&& source ~/.zshrc
```

配置 tldr

```
┌──(root@debian)-[~]
└─# mkdir -p /root/.local/share/tldr \
&& apt install -y tldr \
&& tldr -u
```

创建目录

```
┌──(root@debian)-[~]
└─# mkdir -p \
/root/tools/apps \
/root/tools/drivers \
/root/tools/scripts \
/var/www/html/upload
```

关机，拍摄快照并命名为 `初始化` 

```
┌──(root@debian)-[~]
└─# init 0
```

## 5. Deploy

|                             环境                             |
| :----------------------------------------------------------: |
| [proxy](https://github.com/jadensalas469466/tools/blob/main/other/proxy.sh) |
|               [Xray](https://xtls.github.io/)                |
|  [Proxychains-NG](https://github.com/rofl0r/proxychains-ng)  |
|      [Tor](https://gitlab.torproject.org/tpo/core/tor)       |
|              [Git](https://github.com/git/git)               |
|              [Python](https://www.python.org/)               |
|                    [Go](https://go.dev/)                     |
|              [Docker](https://www.docker.com/)               |
|           [MongoDB](https://www.mongodb.com/zh-cn)           |
|        [glow](https://github.com/charmbracelet/glow)         |

|                            靶场                             |
| :---------------------------------------------------------: |
| [Pikachu](https://github.com/zhuifengshaonianhanlu/pikachu) |
|          [DVWA](https://github.com/digininja/DVWA)          |
|         [Vulhub](https://github.com/vulhub/vulhub)          |

|                             工具                             |
| :----------------------------------------------------------: |
|      [subfinder](https://www.kali.org/tools/subfinder/)      |
|          [naabu](https://www.kali.org/tools/naabu/)          |
|      [httpx](https://www.kali.org/tools/httpx-toolkit/)      |
|    [cdnNone](https://github.com/jadensalas469466/cdnNone)    |
|      [ipGet](https://github.com/jadensalas469466/ipGet)      |
| [hostCollision](https://github.com/alwaystest18/hostCollision) |
|        [whatweb](https://www.kali.org/tools/whatweb/)        |
|  [observer_ward](https://github.com/emo-crab/observer_ward)  |
|      [EHole](https://github.com/EdgeSecurityTeam/EHole)      |
|         [Finger](https://github.com/EASY233/Finger)          |
|          [nikto](https://www.kali.org/tools/nikto/)          |
|         [nuclei](https://www.kali.org/tools/nuclei/)         |
|           [ffuf](https://www.kali.org/tools/ffuf/)           |

|                      server                      |
| :----------------------------------------------: |
|       [Project X](https://xtls.github.io/)       |
|        [UFW](https://github.com/jbq/ufw)         |
| [fail2ban](https://github.com/fail2ban/fail2ban) |
|        [Tor](https://www.torproject.org/)        |
|       [Syncthing](https://syncthing.net/)        |
|  [bind9](https://github.com/isc-projects/bind9)  |

## 6 使用

### 6.1. 配置无线网卡驱动

查看内核版本

```
┌──(root@debian)-[~]
└─# uname -r
6.5.0-kali3-amd64
```

安装对应的版本

> http://http.kali.org/kali/pool/main/l/linux/

```
┌──(root@debian)-[~]
└─# wget http://http.kali.org/kali/pool/main/l/linux/linux-compiler-gcc-13-x86_6.5.13-1kali2_amd64.deb \
&& dpkg -i linux-compiler-gcc-13-x86_6.5.13-1kali2_amd64.deb \
&& rm -rf linux-compiler-gcc-13-x86_6.5.13-1kali2_amd64.deb
```

安装依赖

```
┌──(root@debian)-[~]
└─# apt install -y build-essential dkms
```

下载驱动

```
┌──(root@debian)-[~]
└─# git clone https://github.com/aircrack-ng/rtl8812au.git /root/tools/drivers/rtl8812au
```

安装驱动

```
┌──(root@debian)-[~]
└─# cd /root/tools/drivers/rtl8812au \
&& make dkms_install \
&& cd
```

> 卸载
>
> ```
> root@debian:~# cd /root/tools/drivers/rtl8812au \
> && make dkms_remove \
> && cd
> ```

### 6.2. 系统信息

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

### 6.3. 挂载共享文件

打开配置文件配置别名

```
┌──(root@debian)-[~]
└─# vim ~/.bashrc
```

```
alias share='vmhgfs-fuse .host:/ /mnt'
```

使配置生效

```
┌──(root@debian)-[~]
└─# source ~/.zshrc
```

### 6.4. 历史命令

> 存储历史命令的文件: `~/.bash_history` 

覆盖历史命令

```
┌──(root@debian)-[~]
└─# shred -z ~/.bash_history \
&& shred -z ~/.zsh_history
```

### 6.5. 后台运行

将命令行程序放在后台运行, 即使 SSH 断开连接也不会终止运行

```
┌──(root@debian)-[~]
└─# nohup <command> > /root/log.txt 2>&1 &
```

```
PID
```

查看后台程序

```
┌──(root@debian)-[~]
└─# jobs
```

> 在当前终端关闭后将失效

实时查看日志

```
┌──(root@debian)-[~]
└─# tail -f /root/log.txt
```

终止进程

```
┌──(root@debian)-[~]
└─# kill <PID>
```

强制终止进程

```
┌──(root@debian)-[~]
└─# kill -9 <PID>
```

### 6.6. 添加多个源并更新为 Kali

导入 Kali 的 GPG 密钥

```
┌──(root@debian)-[~]
└─# curl -fsSL https://archive.kali.org/archive-key.asc \
| tee /etc/apt/trusted.gpg.d/kali.asc
```

配置 `apt` 源

```
┌──(root@debian)-[~]
└─# nano /etc/apt/sources.list
```

```
deb https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main non-free contrib non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ testing main contrib non-free non-free-firmware
```

配置优先级

```
┌──(root@debian)-[~]
└─# nano /etc/apt/preferences
```

```
Package: *
Pin: release o=Kali,a=kali-rolling
Pin-Priority: 900

Package: *
Pin: release o=Debian,a=testing
Pin-Priority: 800
```

获取更新并更新系统

```
┌──(root@debian)-[~]
└─# apt update \
&& apt upgrade \
&& apt dist-upgrade \
&& apt clean \
&& apt autoremove --purge
```

### 6.7. 配置全局代理

```
export http_proxy=socks5://192.168.1.201:10808
export https_proxy=$http_prox
```

---

参考链接

- [Debian](https://www.debian.org/)
- [Debian Docs](https://www.debian.org/doc/)

