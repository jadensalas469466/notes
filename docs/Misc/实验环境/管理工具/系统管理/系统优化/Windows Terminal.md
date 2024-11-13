Windows 上的命令行工具。

# 1 初始化

配置快捷键

![配置快捷键](./../../../../../../images/Windows%20Terminal/%E9%85%8D%E7%BD%AE%E5%BF%AB%E6%8D%B7%E9%94%AE.png)

修改启动大小

![修改启动大小](./../../../../../../images/Windows%20Terminal/%E4%BF%AE%E6%94%B9%E5%90%AF%E5%8A%A8%E5%A4%A7%E5%B0%8F.png)

在启动时居中

![在启动时居中](./../../../../../../images/Windows%20Terminal/%E5%9C%A8%E5%90%AF%E5%8A%A8%E6%97%B6%E5%B1%85%E4%B8%AD.png)

修改主题

![修改主题](./../../../../../../images/Windows%20Terminal/%E4%BF%AE%E6%94%B9%E4%B8%BB%E9%A2%98.png)

始终在通知区域中显示图标

![始终在通知区域中显示图标](./../../../../../../images/Windows%20Terminal/%E5%A7%8B%E7%BB%88%E5%9C%A8%E9%80%9A%E7%9F%A5%E5%8C%BA%E5%9F%9F%E4%B8%AD%E6%98%BE%E7%A4%BA%E5%9B%BE%E6%A0%87.png)

下载 Dracula

> https://github.com/dracula/windows-terminal/

打开 `json` 设置文件

![打开 `settings.json` 设置文件](./../../../../../../images/Windows%20Terminal/%E6%89%93%E5%BC%80%20%60settings.json%60%20%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6.png)

找到 `schemes` 部分并粘贴 `dracula.json` 的内容

```json
    "schemes": 
    [
        {
            "name": "Dracula",
            "cursorColor": "#F8F8F2",
            "selectionBackground": "#44475A",
            "background": "#282A36",
            "foreground": "#F8F8F2",
            "black": "#21222C",
            "blue": "#BD93F9",
            "cyan": "#8BE9FD",
            "green": "#50FA7B",
            "purple": "#FF79C6",
            "red": "#FF5555",
            "white": "#F8F8F2",
            "yellow": "#F1FA8C",
            "brightBlack": "#6272A4",
            "brightBlue": "#D6ACFF",
            "brightCyan": "#A4FFFF",
            "brightGreen": "#69FF94",
            "brightPurple": "#FF92DF",
            "brightRed": "#FF6E6E",
            "brightWhite": "#FFFFFF",
            "brightYellow": "#FFFFA5"
        }
    ],
```

找到 `profiles` 部分并将 `colorScheme` 值添加到默认配置文件中

```json
    "profiles": 
    {
        "defaults": {
            "colorScheme" : "Dracula"
        },
```

修改配色方案并修改字体大小为 18

![修改配色方案并修改字体大小为 18](./../../../../../../images/Windows%20Terminal/%E4%BF%AE%E6%94%B9%E9%85%8D%E8%89%B2%E6%96%B9%E6%A1%88%E5%B9%B6%E4%BF%AE%E6%94%B9%E5%AD%97%E4%BD%93%E5%A4%A7%E5%B0%8F%E4%B8%BA%2018.png)

修改启动目录(改为家目录)

![修改启动目录](./../../../../../../images/Windows%20Terminal/%E4%BF%AE%E6%94%B9%E5%90%AF%E5%8A%A8%E7%9B%AE%E5%BD%95.png)

# 2 使用

配置自定义终端

![配置自定义终端](./../../../../../../images/Windows%20Terminal/%E9%85%8D%E7%BD%AE%E8%87%AA%E5%AE%9A%E4%B9%89%E7%BB%88%E7%AB%AF.png)

---

参考链接

- [Windows Terminal](https://github.com/microsoft/terminal)