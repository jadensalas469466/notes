Syncthing is a continuous file synchronization program.

## 1. Install

### 1.1. Windows

使用默认配置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E4%BD%BF%E7%94%A8%E9%BB%98%E8%AE%A4%E9%85%8D%E7%BD%AE.png)

禁止开机自启和在安装后启动

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E7%A6%81%E6%AD%A2%E5%BC%80%E6%9C%BA%E8%87%AA%E5%90%AF%E5%92%8C%E5%AE%89%E8%A3%85%E5%90%8E%E5%90%AF%E5%8A%A8.png)

报错无法找到脚本引擎 JScript

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E6%8A%A5%E9%94%99%E6%97%A0%E6%B3%95%E6%89%BE%E5%88%B0%E8%84%9A%E6%9C%AC%E5%BC%95%E6%93%8E%20JScript.png)

使用管理员权限重新注册 JScript 引擎

```powershell
PS C:\Users\sec> regsvr32 jscript.dll
```

> 注册成功后将 Syncthing 卸载，重新安装即可

### 1.2. Debian

安装 Syncthing

```
┌──(nemo@debian)-[~]
└─# sudo apt install -y syncthing
```

释放配置文件

```
┌──(nemo@debian)-[~]
└─# sudo cp /lib/systemd/system/syncthing@.service /etc/systemd/system/syncthing@.service
```

允许远程访问

```
┌──(nemo@debian)-[~]
└─# sudo sed -i '/^ExecStart=\/usr\/bin\/syncthing/ s#$# --gui-address="0.0.0.0:8384"#' /etc/systemd/system/syncthing@.service
```

设置防火墙规则, 并重新加载 systemd 系统服务配置文件

```
┌──(nemo@debian)-[~]
└─# sudo ufw allow 8384 && sudo systemctl daemon-reload
```

以 nemo 用户身份启动 Syncthing 服务

```
┌──(nemo@debian)-[~]
└─# sudo systemctl start syncthing@nemo.service
```

若是服务端则

```
┌──(nemo@debian)-[~]
└─# sudo systemctl enable --now syncthing@nemo.service
```

## 2. Init

启动 Syncthing

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E5%90%AF%E5%8A%A8%20Syncthing.png)

使用浏览器访问 Syncthing 控制台

```
https://127.0.0.1:8384/
```

对控制台进行初始化设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E5%AF%B9%E6%8E%A7%E5%88%B6%E5%8F%B0%E8%BF%9B%E8%A1%8C%E5%88%9D%E5%A7%8B%E5%8C%96%E8%AE%BE%E7%BD%AE.png)

常规设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E5%B8%B8%E8%A7%84%E8%AE%BE%E7%BD%AE.png)

图形用户界面设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E5%9B%BE%E5%BD%A2%E7%94%A8%E6%88%B7%E7%95%8C%E9%9D%A2%E8%AE%BE%E7%BD%AE.png)

连接设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%BF%9E%E6%8E%A5%E8%AE%BE%E7%BD%AE.png)

移除默认的文件夹

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E7%A7%BB%E9%99%A4%E9%BB%98%E8%AE%A4%E7%9A%84%E6%96%87%E4%BB%B6%E5%A4%B9.png)

### 2.1. 添加远程设备

在 debian 控制台选择显示 ID

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E5%9C%A8%20debian%20%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%80%89%E6%8B%A9%E6%98%BE%E7%A4%BA%20ID.png)

复制设备标识

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E5%A4%8D%E5%88%B6%E8%AE%BE%E5%A4%87%E6%A0%87%E8%AF%86.png)

在 Windows 控制台添加远程设备

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E5%9C%A8%20Windows%20%E6%8E%A7%E5%88%B6%E5%8F%B0%E6%B7%BB%E5%8A%A0%E8%BF%9C%E7%A8%8B%E8%AE%BE%E5%A4%87.png)

粘贴设备 ID，并设置设备名

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E7%B2%98%E8%B4%B4%E8%AE%BE%E5%A4%87%20ID%EF%BC%8C%E5%B9%B6%E8%AE%BE%E7%BD%AE%E8%AE%BE%E5%A4%87%E5%90%8D.png)

在 debian 控制台接受请求

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E5%9C%A8%20debian%20%E6%8E%A7%E5%88%B6%E5%8F%B0%E6%8E%A5%E5%8F%97%E8%AF%B7%E6%B1%82.png)

### 2.2. 设置文件同步

在控制台添加文件夹

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E5%9C%A8%E6%8E%A7%E5%88%B6%E5%8F%B0%E6%B7%BB%E5%8A%A0%E6%96%87%E4%BB%B6%E5%A4%B9.png)

### 2.2.1. 单向同步

### 2.2.1.1. Windows

常规设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/Windows/%E5%B8%B8%E8%A7%84%E8%AE%BE%E7%BD%AE.png)

共享设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/Windows/%E5%85%B1%E4%BA%AB%E8%AE%BE%E7%BD%AE.png)

文件版本控制设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E6%96%87%E4%BB%B6%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%E8%AE%BE%E7%BD%AE.png)

高级设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/Windows/%E9%AB%98%E7%BA%A7%E8%AE%BE%E7%BD%AE.png)

### 2.2.1.2. Debian

接受请求添加新文件夹

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E6%8E%A5%E5%8F%97%E8%AF%B7%E6%B1%82%E6%B7%BB%E5%8A%A0%E6%96%B0%E6%96%87%E4%BB%B6%E5%A4%B9.png)

常规设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E5%B8%B8%E8%A7%84%E8%AE%BE%E7%BD%AE.png)

共享设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E5%85%B1%E4%BA%AB%E8%AE%BE%E7%BD%AE.png)

文件版本控制设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E6%96%87%E4%BB%B6%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%E8%AE%BE%E7%BD%AE.png)

高级设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E9%AB%98%E7%BA%A7%E8%AE%BE%E7%BD%AE.png)

### 2.2.2 双向同步

### 2.2.2.1. Windows

常规设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/Windows/%E5%B8%B8%E8%A7%84%E8%AE%BE%E7%BD%AE.png)

共享设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/Windows/%E5%85%B1%E4%BA%AB%E8%AE%BE%E7%BD%AE.png)

文件版本控制设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E6%96%87%E4%BB%B6%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%E8%AE%BE%E7%BD%AE.png)

高级设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E9%AB%98%E7%BA%A7%E8%AE%BE%E7%BD%AE.png)

### 2.2.2.2. Debian

常规设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E5%B8%B8%E8%A7%84%E8%AE%BE%E7%BD%AE.png)

共享设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E5%85%B1%E4%BA%AB%E8%AE%BE%E7%BD%AE.png)

文件版本控制设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E6%96%87%E4%BB%B6%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%E8%AE%BE%E7%BD%AE.png)

高级设置

![](./../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E9%AB%98%E7%BA%A7%E8%AE%BE%E7%BD%AE.png)

---

References

- [Syncthing](https://syncthing.net/)
- [如何在 Debian/Ubuntu 上安装 Syncthing进行文件同步备份](https://www.74110.net/tutorial/linux/debian-ubuntu-syncthing/)
