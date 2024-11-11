Syncthing 是一款开源的数据同步工具

## 安装

### Windows

使用默认配置

![使用默认配置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E4%BD%BF%E7%94%A8%E9%BB%98%E8%AE%A4%E9%85%8D%E7%BD%AE.png)

禁止开机自启和在安装后启动

![禁止开机自启和安装后启动](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E7%A6%81%E6%AD%A2%E5%BC%80%E6%9C%BA%E8%87%AA%E5%90%AF%E5%92%8C%E5%AE%89%E8%A3%85%E5%90%8E%E5%90%AF%E5%8A%A8.png)

报错无法找到脚本引擎 JScript

![报错无法找到脚本引擎 JScript](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E6%8A%A5%E9%94%99%E6%97%A0%E6%B3%95%E6%89%BE%E5%88%B0%E8%84%9A%E6%9C%AC%E5%BC%95%E6%93%8E%20JScript.png)

使用管理员权限重新注册 JScript 引擎

```powershell
PS C:\Users\sec> regsvr32 jscript.dll
```

> 注册成功后将 Syncthing 卸载，重新安装即可

### debian

安装 Syncthing

```shell
root@server:~# apt install -y syncthing
```

添加 systemd 系统服务配置文件

```shell
root@server:~# vim /etc/systemd/system/syncthing@.service
```

```
[Unit]
Description=Syncthing - Open Source Continuous File Synchronization for %I
Documentation=man:syncthing(1)
After=network.target
StartLimitIntervalSec=60
StartLimitBurst=4

[Service]
User=%i
ExecStart=/usr/bin/syncthing --no-browser -gui-address="0.0.0.0:8384" --no-restart --logflags=0
Restart=on-failure
RestartSec=1
SuccessExitStatus=3 4
RestartForceExitStatus=3 4

# Hardening
ProtectSystem=full
PrivateTmp=true
SystemCallArchitectures=native
MemoryDenyWriteExecute=true
NoNewPrivileges=true

# Elevated permissions to sync ownership (disabled by default),
# see https://docs.syncthing.net/advanced/folder-sync-ownership
#AmbientCapabilities=CAP_CHOWN CAP_FOWNER

[Install]
WantedBy=multi-user.target
```

> 默认的配置文件模板没有配置远程访问
>
> ```
> /lib/systemd/system/syncthing@.service
> ```

设置防火墙规则

```shell
root@server:~# ufw allow 8384
```

重新加载 systemd 系统服务配置文件

```shell
root@server:~# systemctl daemon-reload
```

以 root 权限启动 Syncthing 服务并设置开机自启

```shell
root@server:~# systemctl enable --now syncthing@root.service
```

## 初始化

使用浏览器访问 Syncthing 控制台

```
https://127.0.0.1:8384/
```

对控制台进行初始化设置

![对控制台进行初始化设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E5%AF%B9%E6%8E%A7%E5%88%B6%E5%8F%B0%E8%BF%9B%E8%A1%8C%E5%88%9D%E5%A7%8B%E5%8C%96%E8%AE%BE%E7%BD%AE.png)

常规设置

![常规设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E5%B8%B8%E8%A7%84%E8%AE%BE%E7%BD%AE.png)

图形用户界面设置

![图形用户界面设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E5%9B%BE%E5%BD%A2%E7%94%A8%E6%88%B7%E7%95%8C%E9%9D%A2%E8%AE%BE%E7%BD%AE.png)

连接设置

![连接设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%BF%9E%E6%8E%A5%E8%AE%BE%E7%BD%AE.png)

编辑默认的文件夹

![编辑默认的文件夹](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E7%BC%96%E8%BE%91%E9%BB%98%E8%AE%A4%E7%9A%84%E6%96%87%E4%BB%B6%E5%A4%B9.png)

移除这个文件夹

![移除这个文件夹](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E7%A7%BB%E9%99%A4%E8%BF%99%E4%B8%AA%E6%96%87%E4%BB%B6%E5%A4%B9.png)

### 添加远程设备

在 debian 控制台选择显示 ID

![在 debian 控制台选择显示 ID](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E5%9C%A8%20debian%20%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%80%89%E6%8B%A9%E6%98%BE%E7%A4%BA%20ID.png)

复制设备标识

![复制设备标识](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E5%A4%8D%E5%88%B6%E8%AE%BE%E5%A4%87%E6%A0%87%E8%AF%86.png)

在 Windows 控制台添加远程设备

![在 Windows 控制台添加远程设备](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E5%9C%A8%20Windows%20%E6%8E%A7%E5%88%B6%E5%8F%B0%E6%B7%BB%E5%8A%A0%E8%BF%9C%E7%A8%8B%E8%AE%BE%E5%A4%87.png)

粘贴设备 ID，并设置设备名

![粘贴设备 ID，并设置设备名](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E7%B2%98%E8%B4%B4%E8%AE%BE%E5%A4%87%20ID%EF%BC%8C%E5%B9%B6%E8%AE%BE%E7%BD%AE%E8%AE%BE%E5%A4%87%E5%90%8D.png)

在 debian 控制台接受请求

![在 debian 控制台接受请求](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E5%9C%A8%20debian%20%E6%8E%A7%E5%88%B6%E5%8F%B0%E6%8E%A5%E5%8F%97%E8%AF%B7%E6%B1%82.png)

### 设置文件同步

在控制台添加文件夹

![在控制台添加文件夹](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E5%9C%A8%E6%8E%A7%E5%88%B6%E5%8F%B0%E6%B7%BB%E5%8A%A0%E6%96%87%E4%BB%B6%E5%A4%B9.png)

#### 单向同步

##### Windows

常规设置

![常规配置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/Windows/%E5%B8%B8%E8%A7%84%E9%85%8D%E7%BD%AE.png)

共享设置

![共享设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/Windows/%E5%85%B1%E4%BA%AB%E8%AE%BE%E7%BD%AE.png)

文件版本控制设置

![文件版本控制设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E6%96%87%E4%BB%B6%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%E8%AE%BE%E7%BD%AE.png)

高级设置

![高级设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/Windows/%E9%AB%98%E7%BA%A7%E8%AE%BE%E7%BD%AE.png)

##### debian

接受请求添加新文件

![接受请求添加新文件夹](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E6%8E%A5%E5%8F%97%E8%AF%B7%E6%B1%82%E6%B7%BB%E5%8A%A0%E6%96%B0%E6%96%87%E4%BB%B6%E5%A4%B9.png)

常规设置

![常规设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E5%B8%B8%E8%A7%84%E8%AE%BE%E7%BD%AE.png)

共享设置

![共享设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E5%85%B1%E4%BA%AB%E8%AE%BE%E7%BD%AE.png)

文件版本控制设置

![文件版本控制设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E6%96%87%E4%BB%B6%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%E8%AE%BE%E7%BD%AE.png)

高级设置

![高级设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E9%AB%98%E7%BA%A7%E8%AE%BE%E7%BD%AE.png)

#### 双向同步

##### Windows

常规设置

![常规配置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/Windows/%E5%B8%B8%E8%A7%84%E9%85%8D%E7%BD%AE.png)

共享设置

![共享设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/Windows/%E5%85%B1%E4%BA%AB%E8%AE%BE%E7%BD%AE.png)

文件版本控制设置

![文件版本控制设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E6%96%87%E4%BB%B6%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%E8%AE%BE%E7%BD%AE.png)

高级设置

![高级设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E9%AB%98%E7%BA%A7%E8%AE%BE%E7%BD%AE.png)

##### debain

常规设置

![常规设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E5%B8%B8%E8%A7%84%E8%AE%BE%E7%BD%AE.png)

共享设置

![共享设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/debian/%E5%85%B1%E4%BA%AB%E8%AE%BE%E7%BD%AE.png)

文件版本控制设置

![文件版本控制设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E6%96%87%E4%BB%B6%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%E8%AE%BE%E7%BD%AE.png)

高级设置

![高级设置](./../../../../../../images/%E9%85%8D%E7%BD%AE%20Syncthing%20%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5/%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E5%90%8C%E6%AD%A5/%E9%AB%98%E7%BA%A7%E8%AE%BE%E7%BD%AE.png)

---

参考链接

- [Syncthing](https://syncthing.net/)
- [如何在 Debian/Ubuntu 上安装 Syncthing进行文件同步备份](https://www.74110.net/tutorial/linux/debian-ubuntu-syncthing/)

