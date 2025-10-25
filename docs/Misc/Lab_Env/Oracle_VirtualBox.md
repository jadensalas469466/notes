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

## 2. Init

创建目录文件

```
┌──(nemo@debian)-[~]
└─$ mkdir -p /home/nemo/Documents/VirtualBox_VMs/ISOs
```

设置虚拟机默认目录

```
/File/Preferences.../Basic/General/Default Machine Folder: /home/nemo/Documents/VirtualBox_VMs
```

手动代理配置

```
/File/Preferences.../Expert/Proxy/Manual Proxy Configuration: http://127.0.0.1:10808
```

### 2.1. 配置 Host-Only Networks

> Host-Only 用于虚拟机之间互相访问

创建一个 Host-only Networks

```
/File/Tools/Network/Create
```

启用 DHCP 服务

```
/File/Tools/Network/Properties/DHCP Server/[V] Enable Server
```

## 3. Usage

端口转发

```
/Machines/VM/Settings/Expert/Network/Adapter 1/Port Forwarding
```

> 推荐设定范围为: 49152-65535

安装增强工具

```
/Machines/VM/Start/Devices/Insert Guest Additions CD images...
```

Network 配置为 Host-only 可被其它虚拟机访问

```
/Machines/VM/Settings/Expert/Network/Adapter 2:
[V] Enable Network Adapter
Attached to: Hoat-only Adapter
```

---

- [Oracle VirtualBox](https://www.virtualbox.org/)
- [Download VirtualBox for Linux Hosts](https://www.virtualbox.org/wiki/Linux_Downloads)
