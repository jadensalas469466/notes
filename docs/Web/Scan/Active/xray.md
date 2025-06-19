Web 漏洞扫描工具.

## 1. Install

修改文件名并添加到环境变量

```
C:\Users\sec\AppData\Local\Programs\xray\xray.exe
```

## 2. 初始化

首次运行时双击程序释放文件

切换到安装目录生成证书

```
PS C:\Users\sec\AppData\Local\Programs\xray> xray genca
```

安装证书到受信任的根证书颁发机构

```
PS C:\Users\sec\AppData\Local\Programs\xray\ca.crt
```

![安装证书到受信任的根证书颁发机构](./../../../../images/xray/%E5%AE%89%E8%A3%85%E8%AF%81%E4%B9%A6%E5%88%B0%E5%8F%97%E4%BF%A1%E4%BB%BB%E7%9A%84%E6%A0%B9%E8%AF%81%E4%B9%A6%E9%A2%81%E5%8F%91%E6%9C%BA%E6%9E%84.png)

删除不允许访问的名单

```
C:\Users\sec\AppData\Local\Programs\xray\config.yaml
```

```yaml
    hostname_disallowed:                # 不允许访问的 Hostname，支持格式如 t.com、*.t.com、1.1.1.1、1.1.1.1/24、1.1-4.1.1-8
    - '*google*'
    - '*github*'
    - '*.gov.cn'
    - '*.edu.cn'
    - '*chaitin*'
    - '*.xray.cool'
```

## 3. 使用

查看帮助

```
xray -h
```

### 3.1. 主动扫描

使用 xray 对靶场进行主动扫描

```
xray webscan --basic-crawler https://example.com --html-output example.html
```

扫描报告会存放在安装目录中

```
C:\Users\sec\AppData\Local\Programs\xray\example.html
```

### 3.2. 被动扫描

在 xray 配置被动扫描

```
xray webscan --listen 127.0.0.1:7777 --html-output scan.html
```

将流量代理到 xray, 可在后台自动扫描

![此时浏览网页，xray 会在后台自动扫描](./../../../../images/xray/%E6%AD%A4%E6%97%B6%E6%B5%8F%E8%A7%88%E7%BD%91%E9%A1%B5%EF%BC%8Cxray%20%E4%BC%9A%E5%9C%A8%E5%90%8E%E5%8F%B0%E8%87%AA%E5%8A%A8%E6%89%AB%E6%8F%8F.png)

### 3.3. 多重代理

### 3.3.1. burp+xray

在 xray 配置被动扫描

```
xray webscan --listen 192.168.1.14:7777 --html-output scan.html
```

在 burp 配置 xray 代理

![在 burp 配置 xray 代理](./../../../../images/xray/%E5%9C%A8%20burp%20%E9%85%8D%E7%BD%AE%20xray%20%E4%BB%A3%E7%90%86.png)

此时会在 burp 和 xray 同时捕获到数据包

![此时会在 burp 和 xray 同时捕获到数据包](./../../../../images/xray/%E6%AD%A4%E6%97%B6%E4%BC%9A%E5%9C%A8%20burp%20%E5%92%8C%20xray%20%E5%90%8C%E6%97%B6%E6%8D%95%E8%8E%B7%E5%88%B0%E6%95%B0%E6%8D%AE%E5%8C%85.png)

### 3.3.2. rad+xray

在 xray 配置被动扫描

```
xray webscan --listen 127.0.0.1:7777 --html-output scan.html
```

配置 xray 代理启动 rad

```
rad -t http://a-centos7-6.local/pikachu/ --http-proxy http://127.0.0.1:7777
```

### 3.3.3. rad+burp+xray

在 xray 配置被动扫描

```
xray webscan --listen 127.0.0.1:7777 --html-output scan.html
```

在 burp 配置 xray 代理

![在 burp 配置 xray 代理](./../../../../images/xray/%E5%9C%A8%20burp%20%E9%85%8D%E7%BD%AE%20xray%20%E4%BB%A3%E7%90%86.png)

配置 burp 代理启动 rad

```
rad -t http://a-centos7-6.local/pikachu/ --http-proxy http://127.0.0.1:8080
```

---

Refrences

- [xray](https://xray.cool/)
