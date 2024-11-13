一款用于 Web 应用漏洞测试的工具。

# 1 初始化

复制 [Fiddler 汉化](https://github.com/jadensalas469466/tools/raw/refs/heads/main/app/other/Fiddler%20%E6%B1%89%E5%8C%96.zip) 中的插件到安装目录

```
Fiddler\FiddlerTexts.txt
Fiddler\Scripts\FdToChinese.dll
```

绕过 AppContainer 限制

![绕过 AppContainer 限制](./../../../images/Fiddler/%E7%BB%95%E8%BF%87%20AppContainer%20%E9%99%90%E5%88%B6.png)

查看监听端口

```
127.0.0.1:8888
```

![查看监听端口](./../../../images/Fiddler/%E6%9F%A5%E7%9C%8B%E7%9B%91%E5%90%AC%E7%AB%AF%E5%8F%A3.png)

设置代理转发

![设置代理转发](./../../../images/Fiddler/%E8%AE%BE%E7%BD%AE%E4%BB%A3%E7%90%86%E8%BD%AC%E5%8F%91.png)

允许远程计算机连接，关闭启动时充当系统代理

```
Capture FTP requests				捕获 FTP 请求
Allow remote computers to connect	允许远程计算机连接
Reuse client connections			重复使用客户端连接
Reuse server connections			重复使用服务器连接
```

```
Act as system proxy on startup		启动时充当系统代理
Monitor all connections 			监控所有连接 
Use PAC Script						使用 PAC 脚本
DefaultLAN							默认局域网
```

![允许远程计算机连接，关闭启动时充当系统代理](./../../../images/Fiddler/%E5%85%81%E8%AE%B8%E8%BF%9C%E7%A8%8B%E8%AE%A1%E7%AE%97%E6%9C%BA%E8%BF%9E%E6%8E%A5%EF%BC%8C%E5%85%B3%E9%97%AD%E5%90%AF%E5%8A%A8%E6%97%B6%E5%85%85%E5%BD%93%E7%B3%BB%E7%BB%9F%E4%BB%A3%E7%90%86.png)

开启解密 HTTPS 流量，并信任证书

```
Capture HTTPS CONNECTs	捕获 HTTPS CONNECT
Decrypt HTTPS traffic	解密 HTTPS 流量
```

![开启解密 HTTPS 流量，并信任证书](./../../../images/Fiddler/%E5%BC%80%E5%90%AF%E8%A7%A3%E5%AF%86%20HTTPS%20%E6%B5%81%E9%87%8F%EF%BC%8C%E5%B9%B6%E4%BF%A1%E4%BB%BB%E8%AF%81%E4%B9%A6.png)

忽略服务器证书错误

```
Ignore server certificate errors (unsafe)	忽略服务器证书错误（不安全）
```

![忽略服务器证书错误](./../../../images/Fiddler/%E5%BF%BD%E7%95%A5%E6%9C%8D%E5%8A%A1%E5%99%A8%E8%AF%81%E4%B9%A6%E9%94%99%E8%AF%AF.png)

信任根证书

```
Trust Root Certificate	信任根证书
```

![信任根证书](./../../../images/Fiddler/%E4%BF%A1%E4%BB%BB%E6%A0%B9%E8%AF%81%E4%B9%A6.png)

> 重启后生效

# 2 使用

配置代理

![配置代理](./../../../images/Fiddler/%E9%85%8D%E7%BD%AE%E4%BB%A3%E7%90%86.png)

---

参考链接

- [Fiddler](https://www.telerik.com/fiddler/fiddler-classic)
