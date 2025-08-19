Display and control your Android device

## 1. Install

解压到 scrcpy 以下目录

```
C:\Users\sec\AppData\Local\Programs\scrcpy
```

## 2. Usage

### 2.1. 有线连接

连续点击多次版本号, 进入开发者模式

开启 `不锁定屏幕` , `USB 调试` 和 `USB调试 (安全设置)` 

将手机和电脑通过 USB 连接, 运行 scrcpy 后即可控制手机

### 2.2. 无线连接

将手机和电脑连接到同一局域网

开启有线连接后开放手机端口

```
PS C:\Users\sec\AppData\Local\Programs\scrcpy> .\adb.exe tcpip 61234
```

开启无线连接

```
PS C:\Users\sec\AppData\Local\Programs\scrcpy> .\adb.exe connect 192.168.1.6:61234
```

运行 scrcpy 后即可控制手机

---

References

- [scrcpy](https://github.com/Genymobile/scrcpy)

