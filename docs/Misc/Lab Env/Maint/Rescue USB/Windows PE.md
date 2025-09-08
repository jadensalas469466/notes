Windows PE (WinPE) is a small operating system used to install, deploy, and repair Windows desktop editions, Windows Server, and other Windows operating systems.

## 1. Download

下载对应的 ADK 和 WinPE 插件

- [Windows ADK for Windows 10, version 2004](https://go.microsoft.com/fwlink/?linkid=2120254)

- [Windows PE add-on for the ADK, version 2004](https://go.microsoft.com/fwlink/?linkid=2120253)

## 2. Install

安装 ADK 到默认路径

```
C:\Program Files (x86)\Windows Kits\10\
```

![安装 ADK 到默认路径](./../../../../../image/Windows%20PE/%E5%AE%89%E8%A3%85%20ADK%20%E5%88%B0%E9%BB%98%E8%AE%A4%E8%B7%AF%E5%BE%84.png)

选择默认安装

安装 WinPE 插件到默认路径

![安装 WinPE 插件到默认路径](./../../../../../image/Windows%20PE/%E5%AE%89%E8%A3%85%20WinPE%20%E6%8F%92%E4%BB%B6%E5%88%B0%E9%BB%98%E8%AE%A4%E8%B7%AF%E5%BE%84.png)

选择默认安装

## 3. Init

将 U 盘连接到电脑

以管理员身份运行部署和映像工具环境

启动 DiskPart

```
C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools>diskpart
```

列出可用磁盘

```
DISKPART> list disk
```

选择可移动磁盘

```
DISKPART> select disk <disk number>
```

清除磁盘

```
DISKPART> clean
```

转换为 MBR 格式

```
DISKPART> convert mbr
```

创建启动分区

```
DISKPART> create partition primary size=2048
```

标记当前分区为活动

```
DISKPART> active
```

格式化当前分区

```
DISKPART> format fs=fat32 quick label="WinPE"
```

为当前分区分配盘符

```
DISKPART> assign
```

创建存储分区

```
DISKPART> create partition primary
```

格式化当前分区

```
DISKPART> format fs=ntfs quick label="Storage"
```

为当前分区分配盘符

```
DISKPART> assign
```

退出 DiskPart

```
DISKPART> exit
```

创建 Windows PE 文件的工作副本

```
C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools>copype amd64 "C:\WinPE_amd64"
```

装载 Windows PE 启动映像

```
C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools>dism /mount-image /imagefile:"C:\WinPE_amd64\media\sources\boot.wim" /index:1 /mountdir:"C:\WinPE_amd64\mount"
```

自定义 Windows PE

```
C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools>dism /add-package /image:"C:\WinPE_amd64\mount" /packagepath:"C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-WMI.cab"

C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools>dism /add-package /image:"C:\WinPE_amd64\mount" /packagepath:"C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-NetFX.cab"

C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools>dism /add-package /image:"C:\WinPE_amd64\mount" /packagepath:"C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-Scripting.cab"

C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools>dism /add-package /image:"C:\WinPE_amd64\mount" /packagepath:"C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-PowerShell.cab"

C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools>dism /add-package /image:"C:\WinPE_amd64\mount" /packagepath:"C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-StorageWMI.cab"
```

卸载 WinPE 映像并提交更改

```
C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools>dism /unmount-image /mountdir:"C:\WinPE_amd64\mount" /commit
```

查看 WinPE 的盘符

```
C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools>wmic logicaldisk where "VolumeName='WinPE'" get DeviceID, VolumeName
```

```
DeviceID VolumeName
E:       WINPE
```

制作 Windows PE 启动盘

```
C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools>makewinpemedia /ufd "C:\WinPE_amd64" "E:"
```

## 4. Usage

常用命令

```
X:\windows\system32>wpeutil shutdown # 关机
X:\windows\system32>wpeutil reboot   # 重启
```

```
PS X:\windows\system32> exit             # 退出 PowerShell
PS X:\windows\system32> stop-computer    # 关机
PS X:\windows\system32> restart-computer # 重启
```

### 4.1. 系统安装

切换为 PowerShell

```
X:\windows\system32>powershell
```

列出所有卷

```
PS X:\windows\system32> get-volume
```

```
DriveLetter FriendlyName
F           Storage
```

列出指定路径下的文件

```
PS X:\windows\system32> ls "F:\Maint\"
```

挂载镜像

```
PS X:\windows\system32> mount-diskimage -imagepath "F:\Maint\windows.iso"
```

```
Attached : True
```

列出所有卷

```
PS X:\windows\system32> get-volume
```

```
DriveLetter FriendlyName
G           CES_X64FREO_EN-US_DV9
```

列出指定路径下的文件

```
PS X:\windows\system32> ls "G:\"
```

运行安装程序

```
PS X:\windows\system32> start-process "G:\setup.exe"
```

---

References

- [Windows PE (WinPE)](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/winpe-intro?view=windows-11)
- [Download and install the Windows ADK](https://learn.microsoft.com/en-us/windows-hardware/get-started/adk-install#other-adk-downloads)
- [Create bootable Windows PE media](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/winpe-create-usb-bootable-drive?view=windows-11)
- [WinPE: Mount and Customize](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/winpe-mount-and-customize?view=windows-11)
