Debian 的程序管理工具。

## 1 帮助

| 操作                | 描述                                                         |
| ------------------- | ------------------------------------------------------------ |
| apt update          | 获取更新                                                     |
| apt search [app]    | 搜索某个程序                                                 |
| apt list            | 列出可用软件                                                 |
| apt search/show     | 搜索软件信息                                                 |
| apt install [app]   | 安装                                                         |
| apt upgrade [app]   | 升级                                                         |
| apt reinstall [app] | 重新安装                                                     |
| apt upgrade         | 保守更新（存在依赖的软件包不予更新，即使版本兼容，建议用于小版本更新） |
| apt dist-upgrade    | 智能更新（存在依赖的软件包会在确认其兼容性后更新，建议用于大版本更新） |
| apt full-upgrade    | 完整更新（完全更新整个系统，忽略兼容性，建议用于大版本更新） |
| apt clean           | 清理所有的软件包                                             |
| apt autoclean       | 清理已安装的软件包                                           |
| apt remove [app]    | 卸载软件（保留配置文件）                                     |
| apt purge [app]     | 卸载软件（不保留配置文件）                                   |
| apt autoremove      | 自动清理孤立的依赖（风险极高）                               |

---

参考链接

- [Apt](https://wiki.debian.org/zh_CN/Apt)