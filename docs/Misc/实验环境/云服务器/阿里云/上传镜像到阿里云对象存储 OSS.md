在阿里云中部署 Kali ，需要上传镜像到阿里云对象存储 OSS。

# 1 初始化

访问凭证管理

![访问凭证管理](./../../../../../images/%E4%B8%8A%E4%BC%A0%E9%95%9C%E5%83%8F%E5%88%B0%E9%98%BF%E9%87%8C%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20OSS/%E8%AE%BF%E9%97%AE%E5%87%AD%E8%AF%81%E7%AE%A1%E7%90%86.png)

创建 AccessKey

![创建 AccessKey](./../../../../../images/%E4%B8%8A%E4%BC%A0%E9%95%9C%E5%83%8F%E5%88%B0%E9%98%BF%E9%87%8C%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20OSS/%E5%88%9B%E5%BB%BA%20AccessKey.png)

# 2 使用

使用 VirtualBox 创建 VHD 格式的镜像文件

下载 cloud-init

```shell
┌──(root㉿kali-23)-[~]
└─# curl -O 'https://ecs-image-tools.oss-cn-hangzhou.aliyuncs.com/cloudinit/debian12/cloud-init_23.2.2-1_all.deb'
```

安装 cloud-init

```shell
┌──(root㉿kali-23)-[~]
└─# sudo apt install -y /root/cloud-init_23.2.2-1_all.deb
```

检查当前操作系统内核是否支持 virtio 驱动

```shell
┌──(root㉿kali-23)-[~]
└─# grep -i virtio /boot/config-$(uname -r)
```

```
CONFIG_VIRTIO_BLK=m
CONFIG_VIRTIO_NET=m
```

> 存在这两行说明支持 virtio 驱动

判断 virtio 驱动是否已添加到临时文件系统

```shell
┌──(root㉿kali-23)-[~]
└─# lsinitramfs /boot/initrd.img-$(uname -r)|grep virtio
```

```
usr/lib/modules/6.5.0-kali3-amd64/kernel/drivers/block/virtio_blk.ko
usr/lib/modules/6.5.0-kali3-amd64/kernel/drivers/net/virtio_net.ko
```

> 存在这两行说明已添加到临时文件系统

使用 ossutil 上传 vhd 镜像文件至目标存储空间

导入镜像

![导入镜像](./../../../../../images/%E4%B8%8A%E4%BC%A0%E9%95%9C%E5%83%8F%E5%88%B0%E9%98%BF%E9%87%8C%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20OSS/%E5%AF%BC%E5%85%A5%E9%95%9C%E5%83%8F.png)

开通对象存储服务OSS 并创建  OSS Bucket

![开通对象存储服务OSS 并创建  OSS Bucket](./../../../../../images/%E4%B8%8A%E4%BC%A0%E9%95%9C%E5%83%8F%E5%88%B0%E9%98%BF%E9%87%8C%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20OSS/%E5%BC%80%E9%80%9A%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%E6%9C%8D%E5%8A%A1OSS%20%E5%B9%B6%E5%88%9B%E5%BB%BA%20%20OSS%20Bucket.png)

上传文件

![上传文件](./../../../../../images/%E4%B8%8A%E4%BC%A0%E9%95%9C%E5%83%8F%E5%88%B0%E9%98%BF%E9%87%8C%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20OSS/%E4%B8%8A%E4%BC%A0%E6%96%87%E4%BB%B6.png)

> 超过 5 GB 使用 ossutil 上传

授予 ECS 对 OSS 资源的访问权限

![授予 ECS 对 OSS 资源的访问权限](./../../../../../images/%E4%B8%8A%E4%BC%A0%E9%95%9C%E5%83%8F%E5%88%B0%E9%98%BF%E9%87%8C%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20OSS/%E6%8E%88%E4%BA%88%20ECS%20%E5%AF%B9%20OSS%20%E8%B5%84%E6%BA%90%E7%9A%84%E8%AE%BF%E9%97%AE%E6%9D%83%E9%99%90.png)

继续导入

![继续导入](./../../../../../images/%E4%B8%8A%E4%BC%A0%E9%95%9C%E5%83%8F%E5%88%B0%E9%98%BF%E9%87%8C%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20OSS/%E7%BB%A7%E7%BB%AD%E5%AF%BC%E5%85%A5.png)

复制文件 URL

![复制文件 URL](./../../../../../images/%E4%B8%8A%E4%BC%A0%E9%95%9C%E5%83%8F%E5%88%B0%E9%98%BF%E9%87%8C%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20OSS/%E5%A4%8D%E5%88%B6%E6%96%87%E4%BB%B6%20URL.png)

导入镜像文件

![导入镜像文件](./../../../../../images/%E4%B8%8A%E4%BC%A0%E9%95%9C%E5%83%8F%E5%88%B0%E9%98%BF%E9%87%8C%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20OSS/%E5%AF%BC%E5%85%A5%E9%95%9C%E5%83%8F%E6%96%87%E4%BB%B6.png)

停机状态下，更换操作系统

![停机状态下，更换操作系统](./../../../../../images/%E4%B8%8A%E4%BC%A0%E9%95%9C%E5%83%8F%E5%88%B0%E9%98%BF%E9%87%8C%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20OSS/%E5%81%9C%E6%9C%BA%E7%8A%B6%E6%80%81%E4%B8%8B%EF%BC%8C%E6%9B%B4%E6%8D%A2%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.png)

更换完成后检查主机名

```shell
┌──(root㉿kali)-[~]
└─# hostname
```

编辑 `/etc/hostname` 文件

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/hostname
```

```
kali-23
```

编辑 `/etc/hosts` 文件

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/hosts
```

```shell
127.0.0.1   localhost
127.0.1.1   kali-23
```

删除 cloud-init 安装包

```shell
┌──(root㉿kali)-[~]
└─# rm -rf cloud-init_23.2.2-1_all.deb
```

> 重启实例

安装 xrdp

```shell
┌──(root㉿kali)-[~]
└─# sudo apt install -y xrdp
```

配置开机自启

```shell
┌──(root㉿kali)-[~]
└─# sudo systemctl enable --now xrdp
```

> 每个账户只允许有一处登录

---

参考链接

- [对象存储 OSS](https://www.aliyun.com/product/oss/)
