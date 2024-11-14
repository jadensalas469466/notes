图形化用户界面操作系统。

# 1 准备

Win11_23H2_Chinese_Simplified_x64v2.iso

```
https://www.microsoft.com/zh-cn/software-download/windows11
```

**物理机**

WePE

```
https://www.wepe.com.cn
```

**虚拟机**

VMware

```
https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion
```

目录

```
C:\Users\sec\Documents\virtual machines\windows
```

# 2 配置

**物理机**

重启系统进入 Boot 菜单

```
需要关闭 Bitlocker
ASUS 是在启动引导界面按 Del 
TinkPad 是在启动引导界面按 F12 
```

选择 U 盘启动进入 WePE

进入 `Win11_23H2_Chinese_Simplified_x64v2.iso` ，运行 `setup.exe` ，进行安装

**虚拟机**

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
Workstation 17.5.x
```

安装来源

```
稍后安装操作系统
```

客户机操作系统

```
Microsoft Windows
```

版本

```
Windows 11 x64
```

虚拟机名称

```
windows
```

位置

```
C:\Users\sec\Documents\virtual machines\windows
```

选择加密类型

```
只有支持 TPM 所需的文件已加密
```

密码生成

```
在此计算机上的凭据管理器中记住密码
```

固件类型

```
UEFI
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
8192 MB
```

网络连接

```
使用桥接网络
```

SCSI 控制器

```
LSI Logic SAS
```

虚拟磁盘类型

```
NVMe
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
C:\Users\sec\Documents\virtual machines\windows\windows.vmdk
```

编辑虚拟机设置

虚拟化引擎

```
虚拟化 Intel VT-x/EPT 或 AMD-V/RVI
```

使用 ISO 映像文件

```
C:\Users\sec\Documents\virtual machines\iso\Win11_23H2_Chinese_Simplified_x64v2.iso
```

3D 图形

```
关闭加速 3D 图形
```

文件夹共享

```
总是启用
```

```
在 Windows 客户机中 映射为网络驱动器
```

添加共享文件夹

主机路径

```
C:\Users\sec\share\vmware
```

名称

```
share
```

其他属性

```
启用此共享
只读
```

拍摄快照并命名为 `配置` 

开启此虚拟机进行安装

# 3 安装

输入语言和其他首选项

```
要安装的语言：中文（简体，中国）
时间和货币格式：中文（简体，中国）
键盘和输入方法：微软拼音
```

现在安装

激活 Windows

```
我没有产品密钥
```

选择要安装的操作系统

```
Windows 11 专业版
```

适用的声明和许可条款

```
我接受 Microsoft 软件许可条款。如果某组织授予许可，则我有权绑定该组织。
```

你想执行哪种类型的安装

```
自定义：仅安装 Windows
```

您想将 Windows 安装在哪里

```
驱动器未分配的空间
```

断开网络连接，按 `Shift+F10` 调出 CMD 跳过联网

```
C:\Windows\System32>oobe\bypassnro
```

这是正确的国家 （地区）吗？

```
美国
```

这种键盘布局是否合适？

```
微软拼音
```

是否要添加第二种键盘布局？

```
添加布局
```

你的第二个键盘布局想使用哪种语言？

```
英语(美国)
```

你要使用哪个键盘布局？

```
美式键盘
```

让我们为你连接到网络

```
我没有 Internet 连接
```

立即连接以快速开始使用你的设备

```
继续执行受限设置
```

谁将使用此设备？

```
物理机: sec
虚拟机: test
```

创建容易记住的密码

```
123456
```

确认你的密码

```
123456
```

为此帐户创建安全问题

```
你第一个宠物的名字是什么？
123456
你出生城市的名称是什么？
123456
你的母校名称是什么？
123456
```

为你的设备选择隐私设置

```
位置：否
查找我的设备：否
诊断数据：否
墨迹书写和输入：否
量身定制的体验：否
广告 ID：否
```

安装网卡驱动，连接网络

关机，拍摄快照并命名为 `安装` 

# 4 初始化

**虚拟机**

安装 VMware Tools

![安装 VMware Tools](./../../../../../../images/Windows%2011/%E5%AE%89%E8%A3%85%20VMware%20Tools.png)

**台式机**

进入控制面板选择高性能模式

![台式机进入控制面板选择高性能模式](./../../../../../../images/Windows%2011/%E5%8F%B0%E5%BC%8F%E6%9C%BA%E8%BF%9B%E5%85%A5%E6%8E%A7%E5%88%B6%E9%9D%A2%E6%9D%BF%E9%80%89%E6%8B%A9%E9%AB%98%E6%80%A7%E8%83%BD%E6%A8%A1%E5%BC%8F.png)

更改计划的设置

![更改计划的设置](./../../../../../../images/Windows%2011/%E6%9B%B4%E6%94%B9%E8%AE%A1%E5%88%92%E7%9A%84%E8%AE%BE%E7%BD%AE.png)

定义电源按钮

![定义电源按钮](./../../../../../../images/Windows%2011/%E5%AE%9A%E4%B9%89%E7%94%B5%E6%BA%90%E6%8C%89%E9%92%AE.png)

**笔记本**

进入控制面板选择高性能模式

更改计划的设置

定义电源按钮 

---

修改设备名称

![虚拟机修改设备名称](./../../../../../../images/Windows%2011/%E8%99%9A%E6%8B%9F%E6%9C%BA%E4%BF%AE%E6%94%B9%E8%AE%BE%E5%A4%87%E5%90%8D%E7%A7%B0.png)

设置为专用网络并分配 IP 和 DNS

```
IPv4：开
IP 地址：192.168.1.201 (台式机)
IP 地址：192.168.1.202 (笔记本)
子网掩码：255.255.255.0
网关：192.168.1.1
首选 DNS：8.8.8.8
DNS over HTTPS：开(自动模板)
DNS over HTTPS 模板：https://dns.google/dns-query
失败时使用未加密请求：开
备用 DNS：1.1.1.1
DNS over HTTPS：开(自动模板)
DNS over HTTPS 模板：https://one.one.one.one/dns-query
失败时使用未加密请求：开
```

修改 `hosts` 文件

```
C:\Windows\System32\drivers\etc\hosts
```

使用 Office Tool Plus 安装 Office

使用 MAS 激活 Windows 和 Office

使用 Geek 卸载不需要的应用

安全中心添加排除项

更新驱动、系统和应用

设置 Windows、Edge 和 Office

创建文件夹

```
C:\Users\sec
├─Documents
│	├─KeePass
│	└─VeraCrypt
│		└─iso
├─Pictures
|	└─截图
└─share
	├─github
	└─VMware
```

关机，快照命名为 `初始化` 

# 5 部署

|                            虚拟机                            |
| :----------------------------------------------------------: |
|               [7-Zip](https://www.7-zip.org/)                |
|             [Geek](https://geekuninstaller.com/)             |
| [OpenSSH](https://learn.microsoft.com/zh-cn/windows-server/administration/openssh/openssh_install_firstuse?tabs=powershell) |
|                [phpStudy](https://www.xp.cn/)                |

关机，快照命名为 `部署` 

---

参考链接

- [Windows](https://learn.microsoft.com/zh-cn/windows/)

