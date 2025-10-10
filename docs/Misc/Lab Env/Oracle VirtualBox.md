VirtualBox is a general-purpose full virtualization software for x86_64 hardware (with version 7.1 additionally for macOS/Arm), targeted at laptop, desktop, server and embedded use.

## 1. Install

导入公钥

```
┌──(nemo@debian)-[~]
└─$ wget -O- https://www.virtualbox.org/download/oracle_vbox_2016.asc | sudo gpg --yes --output /usr/share/keyrings/oracle-virtualbox-2016.gpg --dearmor
```

添加仓库

```
┌──(nemo@debian)-[~]
└─$ echo "deb [arch=amd64 signed-by=/usr/share/keyrings/oracle-virtualbox-2016.gpg] https://download.virtualbox.org/virtualbox/debian $(lsb_release -cs) contrib" | sudo tee /etc/apt/sources.list.d/virtualbox.list
```

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt update && sudo apt install -y virtualbox
```

禁用 VirtualBox Python Support

![](./../../../images/Oracle%20VirtualBox/%E7%A6%81%E7%94%A8%20VirtualBox%20Python%20Support.png)

不在桌面创建快捷方式

![](./../../../images/Oracle%20VirtualBox/%E4%B8%8D%E5%9C%A8%E6%A1%8C%E9%9D%A2%E5%88%9B%E5%BB%BA%E5%BF%AB%E6%8D%B7%E6%96%B9%E5%BC%8F.png)

## 2. Init

创建目录文件

```
┌──(nemo@debian)-[~]
└─$ mkdir -p /home/nemo/virtualbox-vms/iso
```

```
C:\Users\nemo\VirtualBox VMs\iso
```

设置默认目录

```
/File/Preferences.../Basic/General/Default Machine Folder: /home/nemo/virtualbox-vms
```

```
/File/Preferences.../Basic/General/Default Machine Folder: C:\Users\nemo\VirtualBox VMs
```

Manual Proxy Configuration

![](./../../../images/Oracle%20VirtualBox/Manual%20Proxy%20Configuration.png)

### 2.1. 配置 Host-Only Networks

> Host-Only 用于虚拟机之间互相访问

打开 File - Tools - Network

![](./../../../images/Oracle%20VirtualBox/%E6%89%93%E5%BC%80%20File%20-%20Tools%20-%20Network.png)

创建一个 Host-only Networks

![](./../../../images/Oracle%20VirtualBox/%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%20Host-only%20Networks.png)

DHCP Server

![](./../../../images/Oracle%20VirtualBox/DHCP%20Server.png)

## 3. Usage

Port Forwarding

> 推荐设定范围为: 49152-65535

![](./../../../images/Oracle%20VirtualBox/Port%20Forwarding.png)

Insert Guest Additions CD images

![](./../../../images/Oracle%20VirtualBox/Insert%20Guest%20Additions%20CD%20image.png)

Network 配置为 Host-only 可被其它虚拟机访问

![](./../../../images/Oracle%20VirtualBox/Network%20%E9%85%8D%E7%BD%AE%E4%B8%BA%20Host-only%20%E5%8F%AF%E8%A2%AB%E5%85%B6%E5%AE%83%E8%99%9A%E6%8B%9F%E6%9C%BA%E8%AE%BF%E9%97%AE.png)

---

- [Oracle VirtualBox](https://www.virtualbox.org/)
- [Download VirtualBox for Linux Hosts](https://www.virtualbox.org/wiki/Linux_Downloads)
