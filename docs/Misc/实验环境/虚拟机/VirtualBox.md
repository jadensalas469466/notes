

# 1 初始化

修改默认虚拟机位置

```
C:\Users\sec\Documents\Virtual Machines
```

![修改默认虚拟机位置](./../../../../images/VirtualBox/%E4%BF%AE%E6%94%B9%E9%BB%98%E8%AE%A4%E8%99%9A%E6%8B%9F%E6%9C%BA%E4%BD%8D%E7%BD%AE.png)

# 2 使用

## 2.1 拍摄快照

拍摄系统快照

![拍摄系统快照](./../../../../images/VirtualBox/%E6%8B%8D%E6%91%84%E7%B3%BB%E7%BB%9F%E5%BF%AB%E7%85%A7.png)

## 2.2 配置代理

配置代理

![配置代理](./../../../../images/VirtualBox/%E9%85%8D%E7%BD%AE%E4%BB%A3%E7%90%86.png)

## 2.3 创建 VHD 镜像

根据服务器配置创建虚拟机

![根据服务器配置创建虚拟机](./../../../../images/VirtualBox/%E6%A0%B9%E6%8D%AE%E6%9C%8D%E5%8A%A1%E5%99%A8%E9%85%8D%E7%BD%AE%E5%88%9B%E5%BB%BA%E8%99%9A%E6%8B%9F%E6%9C%BA.png)

> CPU 根据 vCPU 数量设置
>
> 内存和硬盘文件大小与实例相同
>
> 文件类型使用 VHD

分配光驱

![分配光驱](./../../../../images/VirtualBox/%E5%88%86%E9%85%8D%E5%85%89%E9%A9%B1.png)

> 选择第一IDE控制器主通道

配置网络

![配置网络](./../../../../images/VirtualBox/%E9%85%8D%E7%BD%AE%E7%BD%91%E7%BB%9C.png)

> 启动虚拟机，参照 kali 安装即可

> 安装后在 root 配置 ssh 并根据云服务器的需求配置

## 2.4 转换镜像格式

将 `kali-23.qcow` 复制到 VirtualBox 安装目录

```
C:\Users\sec\VirtualBox VMs\kali-23\kali-23.qcow
D:\software\VirtualBox\kali-23.qcow
```

在 VirtualBox 安装目录中将 kali.qcow 转换为 kali.raw

```powershell
PS D:\software\VirtualBox> .\VBoxManage clonehd -format RAW .\kali-23.qcow .\kali-23.raw
```

---

参考链接

- [VirtualBox](https://www.virtualbox.org/)
- [VirtualBox Documentation](https://www.virtualbox.org/wiki/Documentation)
