Display and control your Android device

## 1. Install

解压到 scrcpy 以下目录并添加到环境变量

```
C:\Users\sec\AppData\Local\Programs\scrcpy
```

## 2. Usage

### 2.1. 有线连接

连续点击多次版本号, 进入开发者模式

开启 `不锁定屏幕` , `USB 调试` 和 `USB调试 (安全设置)` 

将手机和电脑通过 USB 连接后运行

```
PS C:\Users\sec> scrcpy
```

### 2.2. 无线连接

将手机和电脑连接到同一局域网

开启有线连接后开放手机端口

```
PS C:\Users\sec> adb tcpip 61234
```

开启无线连接

```
PS C:\Users\sec> adb connect 192.168.0.50:61234
```

运行 scrcpy

```
PS C:\Users\sec> scrcpy
```

---

References

- [scrcpy](https://github.com/Genymobile/scrcpy)

