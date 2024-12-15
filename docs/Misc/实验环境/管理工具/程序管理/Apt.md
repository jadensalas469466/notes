Debian 的程序管理工具。

## 1 帮助

常用命令

```
apt list              # 列出已安装软件
apt update            # 获取更新
apt search <some-app> # 搜索软件
apt show <some-app>   # 显示软件信息
```

软件管理

```
apt install <some-app>                # 安装软件
apt reinstall <some-app>              # 重装软件
apt install --only-upgrade <some-app> # 升级软件
```

系统更新

```
apt upgrade      # 保守更新 (存在依赖的软件包不予更新，即使版本兼容，建议用于小版本更新)
apt dist-upgrade # 智能更新 (存在依赖的软件包会在确认其兼容性后更新，建议用于大版本更新)
apt full-upgrade # 完整更新 (完全更新整个系统，忽略兼容性，建议用于大版本更新)
```

软件卸载

```
apt remove <some-app>  # 卸载软件 (保留配置文件)
apt purge <some-app>   # 卸载软件 (不保留配置文件)
apt autoremove         # 自动删除未使用的安装包 (保留配置文件)
apt autoremove --purge # 自动删除未使用的安装包 (不保留配置文件)
```

---

参考链接

- [apt](https://wiki.debian.org/zh_CN/Apt)