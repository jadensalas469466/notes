一个 Office 部署工具

## 1 部署

配置部署

![配置部署](./../../../../../../../images/Office%20Tool%20Plus/%E9%85%8D%E7%BD%AE%E9%83%A8%E7%BD%B2.png)

添加产品

![添加产品](./../../../../../../../images/Office%20Tool%20Plus/%E6%B7%BB%E5%8A%A0%E4%BA%A7%E5%93%81.png)

选择产品

```
Office LTSC 专业增强版 2024 -批量许可证
Visio LTSC 专业版 2024 -批量许可证
```

![选择产品](./../../../../../../../images/Office%20Tool%20Plus/%E9%80%89%E6%8B%A9%E4%BA%A7%E5%93%81.png)

选择应用程序

![选择应用程序](./../../../../../../../images/Office%20Tool%20Plus/%E9%80%89%E6%8B%A9%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F.png)

> 保留 Excel、PowerPoint、Visio、Word，由于 Visio 是单独的产品，不需要选择

添加语言

![添加语言](./../../../../../../../images/Office%20Tool%20Plus/%E6%B7%BB%E5%8A%A0%E8%AF%AD%E8%A8%80.png)

开始部署

![开始部署](./../../../../../../../images/Office%20Tool%20Plus/%E5%BC%80%E5%A7%8B%E9%83%A8%E7%BD%B2.png)

## 2 激活

### 2.1 使用 [Microsoft-Activation-Scripts](https://github.com/massgravel/Microsoft-Activation-Scripts) 激活

```powershell
PS C:\Windows\system32> irm https://get.activated.win | iex
```

| 激活类型   | 支持的产品           | 激活期限                 |
| :--------- | :------------------- | :----------------------- |
| HWID       | Windows 10-11        | 永久                     |
| Ohook      | Office               | 永久                     |
| KMS38      | Windows 10-11-Server | 到 2038 年               |
| Online KMS | Windows / Office     | 180 天。终身，有续费任务 |

### 2.2 使用 Office Tool Plus 激活

获取主机名

>https://www.coolhub.top/tech-articles/kms_list.html

![获取主机名](./../../../../../../../images/Office%20Tool%20Plus/%E8%8E%B7%E5%8F%96%E4%B8%BB%E6%9C%BA%E5%90%8D.png)

清除激活信息

![清除激活信息](./../../../../../../../images/Office%20Tool%20Plus/%E6%B8%85%E9%99%A4%E6%BF%80%E6%B4%BB%E4%BF%A1%E6%81%AF.png)

卸载所有产品密钥

![卸载所有产品密钥](./../../../../../../../images/Office%20Tool%20Plus/%E5%8D%B8%E8%BD%BD%E6%89%80%E6%9C%89%E4%BA%A7%E5%93%81%E5%AF%86%E9%92%A5.png)

安装对应的许可证

![安装对应的许可证](./../../../../../../../images/Office%20Tool%20Plus/%E5%AE%89%E8%A3%85%E5%AF%B9%E5%BA%94%E7%9A%84%E8%AE%B8%E5%8F%AF%E8%AF%81.png)

激活

![激活](./../../../../../../../images/Office%20Tool%20Plus/%E6%BF%80%E6%B4%BB.png)

成功

![成功](./../../../../../../../images/Office%20Tool%20Plus/%E6%88%90%E5%8A%9F.png)

> 若不成功则更换 KMS 主机再次尝试

---

参考链接

- [Office Tool Plus](https://github.com/YerongAI/Office-Tool)
- [Office Tool Plus Documentation](https://www.officetool.plus/zh-cn/)
