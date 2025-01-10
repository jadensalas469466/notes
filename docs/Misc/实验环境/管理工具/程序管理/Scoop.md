用于 Windows 的命令行安装程序.

## 1. 安装

更改执行策略, 允许所有脚本运行

```
PS C:\Users\sec> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

下载并执行 Scoop 安装脚本

```
PS C:\Users\sec> irm get.scoop.sh -Proxy 'http://127.0.0.1:10808' | iex
```

## 2. 初始化

配置代理

```
scoop config proxy 127.0.0.1:10808
```

安装基础工具

```
scoop install aria2 7zip git
```

添加 SPC Bucket

```
scoop bucket add spc https://github.com/lzwme/scoop-proxy-cn
```

安装常用工具

```
scoop install sudo scoop-search vim sdelete python
```

## 3. 部署

|                            scoop                             |
| :----------------------------------------------------------: |
|              [aria2](https://aria2.github.io/)               |
|                [7zip](https://www.7-zip.org/)                |
|                 [git](https://git-scm.com/)                  |
|          [gsudo](https://github.com/gerardog/gsudo)          |
|  [scoop-search](https://github.com/tokiedokie/scoop-search)  |
| [sdelete](https://learn.microsoft.com/zh-cn/sysinternals/downloads/sdelete) |
|                 [vim](https://www.vim.org/)                  |
|              [python](https://www.python.org/)               |

## 4. 使用

查看帮助

```
scoop help           # 可用命令
scoop help [list-command] # 获取特定命令的更多帮助
```

软件状态

```
scoop list   # 列出已装软件
scoop status # 检查已装软件更新
```

软件检索

```
scoop search SomeSoftware # 使用官方较慢的搜索
scoop-search SomeSoftware # 使用第三方快速搜索
```

软件安装

```
scoop install SomeSoftware                  # 普通安装
sudo scoop install SomeSoftware             # 管理员权限安装
scoop install SomeSoftware@[version-number] # 指定版本安装
sudo scoop install SomeSoftware --global    # 全局安装
scoop install bucket/SomeSoftware           # 从指定 Bucket 安装
```

软件更新

```
scoop update              # 更新 Scoop
scoop update *            # 更新全部软件
scoop update SomeSoftware # 更新指定软件
```

软件卸载

```
scoop uninstall SomeSoftware  # 卸载软件
scoop uninstall scoop         # 卸载 Scoop 及其安装的程序 (需要管理员权限)
```

清理缓存

```
scoop cache show              # 查看所有缓存
scoop cache rm *              # 清理所有缓存
scoop cache rm SomeSoftware   # 清理指定软件的缓存
```

过期软件

```
scoop cleanup SomeSoftware    # 卸载指定的过期软件，保留最新版
scoop cleanup SomeSoftware -a # 卸载全部的过期软件，保留最新版
scoop cleanup SomeSoftware -g # 卸载过期的全局软件，保留最新版
scoop cleanup SomeSoftware -k # 删除过期软件的下载缓存
```

代理配置

```
scoop config proxy 127.0.0.1:10808 # 添加代理
scoop config rm proxy              # 删除代理
```

配置 Bucket

```
scoop bucket rm main                                         # 删除 Bucket
scoop bucket add main https://github.com/ScoopInstaller/Main # 添加 Bucket
```

镜像加速

```
scoop config scoop_repo https://ghp.ci/github.com/ScoopInstaller/Scoop # 配置 ScoopRepo 镜像加速
scoop bucket add main https://ghp.ci/github.com/ScoopInstaller/Main    # 配置 Bucket 镜像加速
```

---

参考链接

- [scoop](https://scoop.sh/)