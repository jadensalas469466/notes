Web 服务指纹识别工具.

## 1. 安装

下载

```
┌──(root@debian)-[~]
└─# curl -LO https://github.com/emo-crab/observer_ward/releases/download/v2024.11.5/observer-ward_v2024.11.5_x86_64-unknown-linux-musl.deb
```

安装

```
┌──(root@debian)-[~]
└─# apt install ./observer-ward_v2024.11.5_x86_64-unknown-linux-musl.deb && rm -rf ./observer-ward_v2024.11.5_x86_64-unknown-linux-musl.deb
```

## 2. 初始化

更新指纹

```
┌──(root@debian)-[~]
└─# observer_ward -u
```

## 3. 使用

识别目标使用的 Web 服务

```
observer_ward -t <target-url> -o fileName.txt
```

更新

```
observer_ward -u              # 更新指纹
observer_ward --update-self   # 更新程序
```

---

参考链接

- [observer_ward](https://github.com/emo-crab/observer_ward)