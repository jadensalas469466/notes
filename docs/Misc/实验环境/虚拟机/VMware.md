用于创建和管理虚拟机的软件。

# 1 下载

最新的 VMware 下载需要登录，可直接从 VMware 的 CDS 服务器下载

> https://softwareupdate.vmware.com/cds/vmw-desktop/ws/

# 2 部署

安装后选择用于个人用途即可使用

![安装后选择用于个人用途即可使用](./../../../../images/VMware/%E5%AE%89%E8%A3%85%E5%90%8E%E9%80%89%E6%8B%A9%E7%94%A8%E4%BA%8E%E4%B8%AA%E4%BA%BA%E7%94%A8%E9%80%94%E5%8D%B3%E5%8F%AF%E4%BD%BF%E7%94%A8.png)

或者使用商业用途许可证

```
MC60H-DWHD5-H80U9-6V85M-8280D
```

打开首选项

![打开首选项](./../../../../images/VMware/%E6%89%93%E5%BC%80%E9%A6%96%E9%80%89%E9%A1%B9.png)

创建文件夹用于存储镜像

```
C:\Users\sec\Documents\Virtual Machines\ISO
```

取消自适应窗口

![取消自适应窗口](./../../../../images/VMware/%E5%8F%96%E6%B6%88%E8%87%AA%E9%80%82%E5%BA%94%E7%AA%97%E5%8F%A3.png)

**配置虚拟网络**

打开虚拟网络编辑器

![打开虚拟网络编辑器](./../../../../images/VMware/%E6%89%93%E5%BC%80%E8%99%9A%E6%8B%9F%E7%BD%91%E7%BB%9C%E7%BC%96%E8%BE%91%E5%99%A8.png)

更改设置

![更改设置](./../../../../images/VMware/%E6%9B%B4%E6%94%B9%E8%AE%BE%E7%BD%AE.png)

桥接模式

![桥接模式](./../../../../images/VMware/%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F.png)

仅主机模式

![仅主机模式](./../../../../images/VMware/%E4%BB%85%E4%B8%BB%E6%9C%BA%E6%A8%A1%E5%BC%8F.png)

NAT 模式

![NAT 模式](./../../../../images/VMware/NAT%20%E6%A8%A1%E5%BC%8F.png)

# 3 使用

风险文件夹

```
C:\Users\sec\AppData\Local\Temp\vmware-sec\VMwareDnD
```

进入 `bios` 

![进入 bios](./../../../../images/VMware/%E8%BF%9B%E5%85%A5%20bios.png)

虚拟机内打开安全选项 `Ctrl + Alt + Ins` 

![虚拟机内打开安全选项](./../../../../images/VMware/%E8%99%9A%E6%8B%9F%E6%9C%BA%E5%86%85%E6%89%93%E5%BC%80%E5%AE%89%E5%85%A8%E9%80%89%E9%A1%B9.png)

清理磁盘

![清理磁盘](./../../../../images/VMware/%E6%B8%85%E7%90%86%E7%A3%81%E7%9B%98.png)

**共享文件**

创建共享文件夹

```
C:\Users\sec\Share\VMware
```

启用文件夹共享

![启用文件夹共享](./../../../../images/VMware/%E5%90%AF%E7%94%A8%E6%96%87%E4%BB%B6%E5%A4%B9%E5%85%B1%E4%BA%AB.png)

添加共享用户

![添加共享用户](./../../../../images/VMware/%E6%B7%BB%E5%8A%A0%E5%85%B1%E4%BA%AB%E7%94%A8%E6%88%B7.png)

导出为 OVF

![导出为 OVF](./../../../../images/VMware/%E5%AF%BC%E5%87%BA%E4%B8%BA%20OVF.png)

---

参考链接

- [VMware](https://www.vmware.com/)
- [VMware Documentation](https://docs.vmware.com/cn/)