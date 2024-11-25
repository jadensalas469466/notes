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

