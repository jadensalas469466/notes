阿里云对象存储 OSS 的命令行工具。

## 1 初始化

创建配置文件

```powershell
PS D:\downloads\ossutil-v1.7.18-windows-amd64> .\ossutil config
```

```
请输入配置文件名,文件名可以带路径(默认为：C:\\Users\sec\.ossutilconfig，回车将使用默认配置文件。如果用户设置为其它文件，在使用命令时需要将--config-file选项设置为该文件）：
未输入配置文件，将使用默认配置文件：C:\\Users\sec\.ossutilconfig。

对于下述配置，回车将跳过相关配置项的设置，配置项的具体含义，请使用"help config"命令查看。
请输入语言(CH/EN，默认为：CH，该配置项将在此次config命令成功结束后生效)：
请输入accessKeyID：
请输入accessKeySecret：
请输入stsToken：
请输入endpoint：https://oss-cn-beijing.aliyuncs.com
```

> 在阿里云中获得 `accessKeyID` 和 `accessKeySecret` 
>
>  `stsToken` 留空即可

## 2 使用

上传文件 `kali-23.vhd` 至目标存储空间 `oss://bucket-beijing-kali/` 

```powershell
PS D:\downloads\ossutil-v1.7.18-windows-amd64> .\ossutil cp kali-23.vhd oss://bucket-beijing-kali/ --endpoint oss-cn-beijing.aliyuncs.com
```

## 3 帮助

```powershell
PS D:\downloads\ossutil-v1.7.18-windows-amd64> .\ossutil help
```

---

参考链接

- [Aliyun OSSUTIL](https://github.com/aliyun/ossutil)
