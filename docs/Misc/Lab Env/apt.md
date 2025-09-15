Debian 的程序管理工具.

## 1. use

常用命令

```
sudo apt list              # 列出已安装软件
sudo apt update            # 获取更新
sudo apt search <some_app> # 搜索软件
sudo apt show <some_app>   # 显示软件信息
```

软件安装

```
sudo apt install <some_app>                       # 安装软件
sudo apt install <some_app> -t bookworm-backports # 指定软件源安装
sudo apt reinstall <some_app>              # 重装软件
sudo apt install --only-upgrade <some_app> # 升级软件
```

系统更新

```
sudo apt upgrade      # 保守更新 (存在依赖的软件包不予更新，即使版本兼容，建议用于小版本更新)
sudo apt dist-upgrade # 智能更新 (存在依赖的软件包会在确认其兼容性后更新，建议用于大版本更新)
sudo apt full-upgrade # 完整更新 (完全更新整个系统，忽略兼容性，建议用于大版本更新)
```

软件卸载

```
sudo apt remove <some_app>  # 卸载软件 (保留配置文件)
sudo apt purge <some_app>   # 卸载软件 (不保留配置文件)
```

安装包清理

```
sudo apt clean              # 删除所有的安装包
sudo apt autoclean          # 删除已过期的安装包
sudo apt autoremove         # 自动删除未使用的依赖 (保留配置文件)
sudo apt autoremove --purge # 自动删除未使用的依赖 (不保留配置文件)
```

---

References

- [apt](https://wiki.debian.org/zh_CN/Apt)