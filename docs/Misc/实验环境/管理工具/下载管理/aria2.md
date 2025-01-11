多线程下载工具.

## 1. 安装

安装

```
scoop install aria2
```

## 2. 使用

配置 16 线程下载

```
aria2 -x 16 "http://example.com/file.zip"
```

配置代理下载

```
aria2 --all-proxy="http://127.0.0.1:10808" "http://example.com/file.zip"
```

经典下载

```
aria2 -x 16 --all-proxy="http://127.0.0.1:10808" "http://example.com/file.zip"
```

