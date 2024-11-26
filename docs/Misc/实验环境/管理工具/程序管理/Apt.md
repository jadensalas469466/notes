Debian 的程序管理工具。

## 1 帮助

常用命令

```
apt list           # 列出已安装软件
apt update         # 获取更新
apt search SomeApp # 搜索软件
apt show SomeApp   # 显示软件信息
```

软件管理

```
apt install SomeApp                # 安装软件
apt reinstall SomeApp              # 重装软件
apt install --only-upgrade SomeApp # 升级软件
```

系统更新

```
apt upgrade      # 保守更新 (存在依赖的软件包不予更新，即使版本兼容，建议用于小版本更新)
apt dist-upgrade # 智能更新 (存在依赖的软件包会在确认其兼容性后更新，建议用于大版本更新)
apt full-upgrade # 完整更新 (完全更新整个系统，忽略兼容性，建议用于大版本更新)
```

缓存清理

```
apt clean     # 清理所有的安装包
apt autoclean # 清理已安装的安装包
```

软件卸载

```
apt remove SomeApp # 卸载软件 (保留配置文件)
apt purge SomeApp  # 卸载软件 (不保留配置文件)
apt autoremove     # 自动卸载孤立的依赖 (风险较高)
```

---

参考链接

- [Apt](https://wiki.debian.org/zh_CN/Apt)