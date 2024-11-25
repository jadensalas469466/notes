用于 Windows 的命令行安装程序。

## 1 部署

更改执行策略，允许所有脚本运行

```powershell
PS C:\Users\sec> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

下载并执行 Scoop 安装脚本

```powershell
PS C:\Users\sec> irm get.scoop.sh -Proxy 'http://127.0.0.1:10809' | iex
```

## 2 初始化

添加代理

```powershell
PS C:\Users\sec> scoop config proxy 127.0.0.1:10809
```

添加 SPC Bucket

```powershell
PS C:\Users\sec> scoop bucket add spc https://github.com/lzwme/scoop-proxy-cn
```

安装依赖

```powershell
PS C:\Users\sec> scoop install 7zip git scoop-search aria2 sudo
```

## 3 使用

查看帮助

```powershell
PS C:\Users\sec> scoop help           # 可用命令
PS C:\Users\sec> scoop help [list-command] # 获取特定命令的更多帮助
```

软件状态

```powershell
PS C:\Users\sec> scoop list   # 列出已装软件
PS C:\Users\sec> scoop status # 检查已装软件更新
```

软件检索

```powershell
PS C:\Users\sec> scoop search SomeSoftware # 使用官方较慢的搜索
PS C:\Users\sec> scoop-search SomeSoftware # 使用第三方快速搜索
```

软件安装

```powershell
PS C:\Users\sec> scoop install SomeSoftware                  # 普通安装
PS C:\Users\sec> sudo scoop install SomeSoftware             # 管理员权限安装
PS C:\Users\sec> scoop install SomeSoftware@[version-number] # 指定版本安装
PS C:\Users\sec> sudo scoop install SomeSoftware --global    # 全局安装
PS C:\Users\sec> scoop install bucket/SomeSoftware           # 从指定 Bucket 安装
```

软件更新

```powershell
PS C:\Users\sec> scoop update              # 更新 Scoop
PS C:\Users\sec> scoop update *            # 更新全部软件
PS C:\Users\sec> scoop update SomeSoftware # 更新指定软件
```

软件卸载

```powershell
PS C:\Users\sec> scoop uninstall SomeSoftware  # 卸载软件
PS C:\Users\sec> scoop uninstall scoop         # 卸载 Scoop 及其安装的程序 (需要管理员权限)
```

清理缓存

```powershell
PS C:\Users\sec> scoop cache show              # 查看所有缓存
PS C:\Users\sec> scoop cache rm *              # 清理所有缓存
PS C:\Users\sec> scoop cache rm SomeSoftware   # 清理指定软件的缓存
```

过期软件

```powershell
PS C:\Users\sec> scoop cleanup SomeSoftware    # 卸载指定的过期软件，保留最新版
PS C:\Users\sec> scoop cleanup SomeSoftware -a # 卸载全部的过期软件，保留最新版
PS C:\Users\sec> scoop cleanup SomeSoftware -g # 卸载过期的全局软件，保留最新版
PS C:\Users\sec> scoop cleanup SomeSoftware -k # 删除过期软件的下载缓存
```

代理配置

```powershell
PS C:\Users\sec> scoop config proxy 127.0.0.1:10809 # 添加代理
PS C:\Users\sec> scoop config rm proxy              # 删除代理
```

配置 Bucket

```powershell
PS C:\Users\sec> scoop bucket rm main                                            # 删除 Bucket
PS C:\Users\sec> scoop bucket add main https://github.com/ScoopInstaller/Main  # 添加 Bucket
```

镜像加速

```powershell
PS C:\Users\sec> scoop config scoop_repo https://ghp.ci/github.com/ScoopInstaller/Scoop  # 配置 ScoopRepo 镜像加速
PS C:\Users\sec> scoop bucket add main https://ghp.ci/github.com/ScoopInstaller/Main    # 配置 Bucket 镜像加速
```

---

参考链接

- [Scoop](https://scoop.sh/)