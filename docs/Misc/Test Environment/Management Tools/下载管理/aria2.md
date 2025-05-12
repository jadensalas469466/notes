aria2 is a lightweight multi-protocol & multi-source command-line download utility.

## 1. 初始化

添加到环境变量

```
C:\Users\sec\AppData\Local\Programs\aria2
```

## 2. 使用

经典下载

```
aria2c -x 16 --all-proxy="http://127.0.0.1:10808" "https://example.com/file_name.zip"
```

配置 16 线程下载

```
aria2c -x 16 "http://example.com/file.zip"
```

配置代理下载

```
aria2c --all-proxy="http://127.0.0.1:10808" "https://example.com/file_name.zip"
```

---

- [aria2](https://aria2.github.io/)
