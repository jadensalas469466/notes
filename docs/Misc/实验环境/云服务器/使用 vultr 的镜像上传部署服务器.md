Vultr 是一个云服务器商，支持直接上传镜像部署服务器

点击 `Add ISO` 

![点击 `Add ISO`](./../../../../images/%E4%BD%BF%E7%94%A8%20vultr%20%E7%9A%84%E9%95%9C%E5%83%8F%E4%B8%8A%E4%BC%A0%E9%83%A8%E7%BD%B2%E6%9C%8D%E5%8A%A1%E5%99%A8/%E7%82%B9%E5%87%BB%20%60Add%20ISO%60.png)

复制链接地址

![复制链接地址](./../../../../images/%E4%BD%BF%E7%94%A8%20vultr%20%E7%9A%84%E9%95%9C%E5%83%8F%E4%B8%8A%E4%BC%A0%E9%83%A8%E7%BD%B2%E6%9C%8D%E5%8A%A1%E5%99%A8/%E5%A4%8D%E5%88%B6%E9%93%BE%E6%8E%A5%E5%9C%B0%E5%9D%80.png)

粘贴，并点击 `Upload` 

![粘贴，并点击 `Upload` ](./../../../../images/%E4%BD%BF%E7%94%A8%20vultr%20%E7%9A%84%E9%95%9C%E5%83%8F%E4%B8%8A%E4%BC%A0%E9%83%A8%E7%BD%B2%E6%9C%8D%E5%8A%A1%E5%99%A8/%E7%B2%98%E8%B4%B4%EF%BC%8C%E5%B9%B6%E7%82%B9%E5%87%BB%20%60Upload%60%20.png)

等待 `ISOs` 中的 `Status` 变为 `Available` 

![等待 `ISOs` 中镜像的 `Status` 变为 `Available` ](./../../../../images/%E4%BD%BF%E7%94%A8%20vultr%20%E7%9A%84%E9%95%9C%E5%83%8F%E4%B8%8A%E4%BC%A0%E9%83%A8%E7%BD%B2%E6%9C%8D%E5%8A%A1%E5%99%A8/%E7%AD%89%E5%BE%85%20%60ISOs%60%20%E4%B8%AD%E9%95%9C%E5%83%8F%E7%9A%84%20%60Status%60%20%E5%8F%98%E4%B8%BA%20%60Available%60%20.png)

点击 `Deploy` 配置服务器

![点击 `Deploy` 配置服务器](./../../../../images/%E4%BD%BF%E7%94%A8%20vultr%20%E7%9A%84%E9%95%9C%E5%83%8F%E4%B8%8A%E4%BC%A0%E9%83%A8%E7%BD%B2%E6%9C%8D%E5%8A%A1%E5%99%A8/%E7%82%B9%E5%87%BB%20%60Deploy%60%20%E9%85%8D%E7%BD%AE%E6%9C%8D%E5%8A%A1%E5%99%A8.png)

Choose Type

```
Cloud Compute - Shared CPU
```

Choose Location

```
Asia:
Singapore
```

Choose Image

```
Upload ISO:
Mv ISOs:
kali-linux-installer-amd64.iso
```

Choose Plan

```
AMD High Performance
```

```
Name: 100 GB NVMe
Cores: 2 vCPUs
Memory: 4 GB
Storage: 100 GB NVMe
Bandwidth: 5 TB
Price: $24/month $0.036/hour
```

关闭 `Auto Backups` 

![关闭 `Auto Backups` ](./../../../../images/%E4%BD%BF%E7%94%A8%20vultr%20%E7%9A%84%E9%95%9C%E5%83%8F%E4%B8%8A%E4%BC%A0%E9%83%A8%E7%BD%B2%E6%9C%8D%E5%8A%A1%E5%99%A8/%E5%85%B3%E9%97%AD%20%60Auto%20Backups%60%20.png)

点击 `Deploy Now` 

![点击 `Deploy Now` ](./../../../../images/%E4%BD%BF%E7%94%A8%20vultr%20%E7%9A%84%E9%95%9C%E5%83%8F%E4%B8%8A%E4%BC%A0%E9%83%A8%E7%BD%B2%E6%9C%8D%E5%8A%A1%E5%99%A8/%E7%82%B9%E5%87%BB%20%60Deploy%20Now%60%20.png)

等待 `Cloud Compute` 中的 `Status` 变为 `Running` 

![等待 `Cloud Compute` 中的 `Status` 变为 `Running` ](./../../../../images/%E4%BD%BF%E7%94%A8%20vultr%20%E7%9A%84%E9%95%9C%E5%83%8F%E4%B8%8A%E4%BC%A0%E9%83%A8%E7%BD%B2%E6%9C%8D%E5%8A%A1%E5%99%A8/%E7%AD%89%E5%BE%85%20%60Cloud%20Compute%60%20%E4%B8%AD%E7%9A%84%20%60Status%60%20%E5%8F%98%E4%B8%BA%20%60Running%60%20.png)

点击 `Running` 

![点击 `Running` ](./../../../../images/%E4%BD%BF%E7%94%A8%20vultr%20%E7%9A%84%E9%95%9C%E5%83%8F%E4%B8%8A%E4%BC%A0%E9%83%A8%E7%BD%B2%E6%9C%8D%E5%8A%A1%E5%99%A8/%E7%82%B9%E5%87%BB%20%60Running%60%20.png)

点击 `View Console` 进行安装

![点击 `View Console` 进行安装](./../../../../images/%E4%BD%BF%E7%94%A8%20vultr%20%E7%9A%84%E9%95%9C%E5%83%8F%E4%B8%8A%E4%BC%A0%E9%83%A8%E7%BD%B2%E6%9C%8D%E5%8A%A1%E5%99%A8/%E7%82%B9%E5%87%BB%20%60View%20Console%60%20%E8%BF%9B%E8%A1%8C%E5%AE%89%E8%A3%85.png)

安装结束后需要在重启前在 `Settings` 中的 `Custom ISO` 点击 `Remove ISO` 移除镜像

---

参考链接

- [Vultr](https://www.vultr.com/)
- [Upload Custom ISO](https://www.vultr.com/features/upload-iso/)

