## 1. MIUI

### 1.1. 绑定账号和设备

连续点击多次版本号, 进入开发者模式

开启 `OEM 解锁` 

在 `设备解锁状态` 中绑定账号和设备

### 1.2. 解锁 bootloader

下载 [miflash_unlock](https://www.miui.com/unlock/download.html) 

> 需要将浏览器设置为中文访问

将手机和电脑通过 USB 连接

在手机开机状态下使用 miflash_unlock 检测并安装驱动后重新连接手机

将手机关机，同时按住开机键和音量下键进入 fastboot 模式

最后使用 miflash_unlock 解锁

---

References

- [root 基础指南](https://www.bilibili.com/video/BV1BY4y1H7Mc/?spm_id_from=333.1387.favlist.content.click&vd_source=2dcc7806c9580af60063ca1edb63852d)
