## 1  升级报错

执行 `scoop update` 报错

```
ERROR 'main' bucket not found. Failed to remove local 'main' bucket.
```

删除 `main` 后重新添加即可

```powershell
PS C:\Users\sec> scoop bucket rm main && scoop bucket add main https://ghp.ci/github.com/ScoopInstaller/Main
```

## 2 Hash 校验错误

安装软件时报错

```
Hash Check Failed.
```

可能是由于软件有更新，忽略即可

```powershell
PS C:\Users\sec> scoop install SomeSoftware -s
```

## 3 镜像加速失效

之前的镜像站 `ghproxy.com` 失效，无法继续下载

配置新的 ScoopRepo 镜像加速

```powershell
PS C:\Users\sec> scoop config scoop_repo https://ghp.ci/github.com/ScoopInstaller/Scoop
```

移除并重新添加 Bucket

```powershell
PS C:\Users\sec> scoop bucket rm spc && scoop bucket add spc https://ghp.ci/github.com/lzwme/scoop-proxy-cn
```

## 4 卸载时的占用问题

使用 `sudo` 卸载 Scoop 会失败

```powershell
PS C:\Users\sec> sudo scoop uninstall scoop
```

![使用 `sudo` 卸载 Scoop 会失败](./../../../images/Scoop%20%E7%9A%84%E4%B8%80%E4%BA%9B%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98/%E4%BD%BF%E7%94%A8%20%60sudo%60%20%E5%8D%B8%E8%BD%BD%20Scoop%20%E4%BC%9A%E5%A4%B1%E8%B4%A5.png)

原因是在 Scoop 卸载时也会对 `sudo` 进行卸载，而 `sudo` 正在使用，出现了文件占用的问题

以管理员身份 PowerShell 运行后卸载即可

```powershell
PS C:\Users\sec> scoop uninstall scoop
```

![以管理员身份 PowerShell 运行后卸载即可](./../../../images/Scoop%20%E7%9A%84%E4%B8%80%E4%BA%9B%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98/%E4%BB%A5%E7%AE%A1%E7%90%86%E5%91%98%E8%BA%AB%E4%BB%BD%20PowerShell%20%E8%BF%90%E8%A1%8C%E5%90%8E%E5%8D%B8%E8%BD%BD%E5%8D%B3%E5%8F%AF.png)
