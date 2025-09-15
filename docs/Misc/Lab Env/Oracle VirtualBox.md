VirtualBox is a general-purpose full virtualization software for x86_64 hardware (with version 7.1 additionally for macOS/Arm), targeted at laptop, desktop, server and embedded use.

## 1. Install

禁用 VirtualBox Python Support

![禁用 VirtualBox Python Support](./../../../images/VirtualBox/%E7%A6%81%E7%94%A8%20VirtualBox%20Python%20Support.png)

不在桌面创建快捷方式

![不在桌面创建快捷方式](./../../../images/VirtualBox/%E4%B8%8D%E5%9C%A8%E6%A1%8C%E9%9D%A2%E5%88%9B%E5%BB%BA%E5%BF%AB%E6%8D%B7%E6%96%B9%E5%BC%8F.png)

## 2. Init

创建目录文件

```
C:\Users\nemo\VirtualBox VMs\iso
```

Manual Proxy Configuration

![Manual Proxy Configuration](./../../../images/VirtualBox/Manual%20Proxy%20Configuration.png)

### 2.1. 配置 Host-only Networks

> Host-only 用于虚拟机之间互相访问

打开 File - Tools - Network

![打开 File - Tools - Network](./../../../images/VirtualBox/%E6%89%93%E5%BC%80%20File%20-%20Tools%20-%20Network.png)

创建一个 Host-only Networks

![创建一个 Host-only Networks](./../../../images/VirtualBox/%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%20Host-only%20Networks.png)

Adapter

![Adapter](./../../../images/VirtualBox/Adapter.png)

DHCP Server

![DHCP Server](./../../../images/VirtualBox/DHCP%20Server.png)

## 3. Usage

Port Forwarding

> 推荐设定范围为: 49152-65535

![Port Forwarding](./../../../images/VirtualBox/Port%20Forwarding.png)

Insert Guest Additions CD images

![Insert Guest Additions CD image](./../../../images/VirtualBox/Insert%20Guest%20Additions%20CD%20image.png)

Network 配置为 Host-only 可被其它虚拟机访问

![Network 配置为 Host-only 可被其它虚拟机访问](./../../../images/VirtualBox/Network%20%E9%85%8D%E7%BD%AE%E4%B8%BA%20Host-only%20%E5%8F%AF%E8%A2%AB%E5%85%B6%E5%AE%83%E8%99%9A%E6%8B%9F%E6%9C%BA%E8%AE%BF%E9%97%AE.png)

---

- [Oracle VirtualBox](https://www.virtualbox.org/)

