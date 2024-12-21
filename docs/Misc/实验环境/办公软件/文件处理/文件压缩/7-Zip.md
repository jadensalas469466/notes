## 1. 部署

安装

```
PS C:\Users\sec> scoop install 7zip
```

## 2. 使用

测试压缩包的完整性

```
7z t /path/fileName.zip
```

列出压缩包内容

```
7z l /path/fileName.zip
```

重命名压缩包中的文件

```
7z rn /path/fileName.zip archivePath/file archivePath/fileRename
```

添加到压缩包

```
7z a /path/fileName.zip /path/             # 将整个目录文件添加到压缩包
7z a /path/fileName.zip /path/ -p          # 将整个目录文件添加到压缩包并添加密码
7z a /path/fileName.zip /path/*            # 将目录下的所有文件添加到压缩包
7z a /path/fileName.zip /path/fileName.txt # 将一个文件添加到压缩包
```

提取文件

```
7z x /path/fileName.zip -o/path/ # 提取文件到指定路径并保留目录结构
7z e /path/fileName.zip -o/path/ # 提取文件到指定路径不保留目录结构
```

---

参考链接

- [7-Zip](https://www.7-zip.org/)