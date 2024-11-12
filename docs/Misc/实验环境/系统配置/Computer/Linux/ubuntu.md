## 准备

ubuntu-live-server-amd64.iso

```
https://cn.ubuntu.com/server
```

VMware

```
https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion
```

目录

```
C:\Users\sec\Documents\virtual machines\ubuntu
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
Ubuntu 64 位
```

虚拟机名称

```
ubuntu
```

位置

```
C:\Users\sec\Documents\virtual machines\ubuntu
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
C:\Users\sec\Documents\virtual machines\ubuntu\ubuntu.vmdk
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
C:\Users\sec\Documents\virtual machines\iso\ubuntu-live-server-amd64.iso
```

显示

```
3D 图形
关闭加速 3D 图形
```

拍摄快照并命名为 `配置` 

## 安装

开启此虚拟机进行安装

GNU GRUB

```
Try or Install Ubuntu Server
```

Welcome

```
[ English ]
```

Installer update available

```
[ Continue without updating ]
```

Keyboard configuration

```
 Layout:    [ English (US) ]
Variant:    [ English (US) ]
```

Choose the type of installation

```
Ubuntu Server
```

Network configuration

```
Default
```

Proxy configuration

```
Proxy address:
```

Ubuntu archive mirror configuration

```
Mirror address:Default
```

Guided storage configuration

```
Set up this disk as an LVM group
```

Storage configuration

```
FILE SYSTEM SUMMARY
		MOUNT POINT			SIZE			TYPE			DEVICE TYPE
	[ /					124.566G		new ext4 	new LVM logical volume ]
	[ /boot				488.000M		new ext4	new LVM logical volume ]
	[ SWAP				976.000M		new swap	new LVM logical volume ]
```

Confirm destructive action

```
Are you sure you want to continue?
[ Continue ]
```

Profile configuration

```
Your name: sec
Your servers name: ubuntu
Pick a username: sec
Chosse a password: 123456
Confirm your password: 123456
```

Upgrade to Ubuntu Pro

```
Skip for now
```

SSH configuration

```
Install OpenSSH server
```

Featured server snaps

```
Default
```

Installation complete

```
Reboot Now
```

按下回车后登录

```
ubuntu login: sec
Password: 123456
```

设置 `root` 用户密码

```shell
sec@ubuntu:~$ sudo passwd root
[sudo] password for sec: 123456
New password: 123456
Retype new password: 123456
passwd: password updated successfully
```

关机，拍摄快照并命名为 `安装` 

```shell
sec@ubuntu:~$ init 0
```

## 初始化

启动虚拟机，使用 `root` 用户登录

**开启 SSH 服务**

允许远程登录 `root` 并配置稳定连接

```shell
root@ubuntu:~# vim /etc/ssh/sshd_config
```

```
 33 PermitRootLogin yes
 99 ClientAliveInterval 60
100 ClientAliveCountMax 60
```

重启 SSH

```shell
root@ubuntu:~# systemctl enable --now ssh.service && systemctl restart ssh.service
```

查看 IP

```shell
root@ubuntu:~# ip addr
```

在 Powershell 远程登录 `root` 

```powershell
PS C:\Users\sec> ssh root@[ip]
```

**修改软件源**

配置 `apt` 源

```shell
root@ubuntu:~# vim /etc/apt/sources.list.d/ubuntu.sources
```

```
Types: deb
URIs: https://mirrors.ustc.edu.cn/ubuntu
Suites: noble noble-updates noble-backports
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

Types: deb
URIs: https://mirrors.ustc.edu.cn/ubuntu
Suites: noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

获取更新

```shell
root@ubuntu:~# apt update
```

安装基础工具

```shell
root@ubuntu:~# apt install -y curl vim net-tools build-essential dkms linux-headers-$(uname -r)
```

**配置网络**

查看网络接口

```shell
root@ubuntu:~# ip link
```

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP mode DEFAULT group default qlen 1000
    link/ether 00:0c:29:21:28:b8 brd ff:ff:ff:ff:ff:ff
    altname enp2s1
```

配置网络接口参数

```shell
root@ubuntu:~# vim /etc/netplan/50-cloud-init.yaml
```

```
# This file is generated from information provided by the datasource.  Changes
# to it will not persist across an instance reboot.  To disable cloud-init's
# network configuration capabilities, write a file
# /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
# network: {config: disabled}
network:
    version: 2
    ethernets:
        ens33:
            dhcp4: no
            addresses:
                - [os_IP]/24
            routes:
                - to: default
                  via: 192.168.1.1
            nameservers:
                addresses:
                    - 8.8.8.8
                    - 1.1.1.1
```

在 `hosts` 文件添加域名映射

```shell
root@ubuntu:~# vim /etc/hosts
```

重启

```shell
root@ubuntu:~# reboot
```

在 Powershell 中删除 SSH 连接缓存

```powershell
PS C:\Users\sec> ssh-keygen -R [ip]
```

远程重新登录 `root` 

```powershell
PS C:\Users\sec> ssh root@ubuntu.local
```

重启后更新缓存并测试网络

```shell
root@ubuntu:~# systemctl restart systemd-resolved && ping g.cn -c 3
```

**创建目录**

```shell
root@ubuntu:~# mkdir -p /root/tool/script /root/tool/driver /var/www/html/upload
```

关机，拍摄快照并命名为 `初始化` 

```shell
root@ubuntu:~# init 0
```

---

参考链接

- [ubuntu](https://cn.ubuntu.com/)

