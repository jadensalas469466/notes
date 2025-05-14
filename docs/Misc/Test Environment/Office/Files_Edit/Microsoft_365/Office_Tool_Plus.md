一个 Office 部署工具.

## 1. 部署

配置部署

![配置部署](C:\Users\sec\share\github\notes\images\Office_Tool_Plus\配置部署.png)

添加产品

```
Office LTSC 专业增强版 2024 -批量许可证
Visio LTSC 专业版 2024 - 批量许可证
```

![添加产品](C:\Users\sec\share\github\notes\images\Office_Tool_Plus\添加产品.png)

选择应用程序

![选择应用程序](C:\Users\sec\share\github\notes\images\Office_Tool_Plus\选择应用程序.png)

> 由于 Visio 是单独的产品, 无需选择;
>
> 保留 Word, Excel, PowerPoint 即可

添加语言

![添加语言](C:\Users\sec\share\github\notes\images\Office_Tool_Plus\添加语言.png)

开始部署

![开始部署](C:\Users\sec\share\github\notes\images\Office_Tool_Plus\开始部署.png)

## 2. 激活

### 2.1. 使用 [Microsoft Activation Scripts (MAS)](https://massgrave.dev/) 激活

```powershell
PS C:\Windows\system32> irm https://get.activated.win | iex
```

### 2.2. 使用 Office Tool Plus 激活

获取主机名

>https://www.coolhub.top/tech-articles/kms_list.html

![获取主机名](C:\Users\sec\share\github\notes\images\Office_Tool_Plus\获取主机名.png)

清除激活信息

![清除激活信息](C:\Users\sec\share\github\notes\images\Office_Tool_Plus\清除激活信息.png)

卸载所有产品密钥

![卸载所有产品密钥](C:\Users\sec\share\github\notes\images\Office_Tool_Plus\卸载所有产品密钥.png)

安装对应的许可证

![安装对应的许可证](C:\Users\sec\share\github\notes\images\Office_Tool_Plus\安装对应的许可证.png)

激活

![激活](C:\Users\sec\share\github\notes\images\Office_Tool_Plus\激活.png)

成功

![成功](C:\Users\sec\share\github\notes\images\Office_Tool_Plus\成功.png)

> 若不成功则更换 KMS 主机再次尝试

---

Refrences

- [Office Tool Plus](https://www.officetool.plus/)
- [Office Tool Plus Documentation](https://www.officetool.plus/zh-cn/)
