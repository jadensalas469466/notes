Web 漏洞扫描工具。

## 1 部署

### 1.1 Kali

下载

```shell
┌──(root㉿kali)-[~]
└─# wget https://github.com/chaitin/xray/releases/download/1.9.11/xray_linux_amd64.zip
```

解压

```shell
┌──(root㉿kali)-[~]
└─# mkdir /root/tools/xray && unzip xray_linux_amd64.zip -d /root/tools/xray && rm -rf xray_linux_amd64.zip
```

编写脚本

```shell
┌──(root㉿kali)-[~]
└─# chmod +x /root/tools/xray/xray_linux_amd64 && vim /root/tools/xray/xray.sh
```

```sh
#!/usr/bin/zsh

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 xray
./xray_linux_amd64 "$@"
```

创建链接

```shell
┌──(root㉿kali)-[~]
└─# chmod +x /root/tools/xray/xray.sh && ln -s /root/tools/xray/xray.sh /usr/local/bin/xray
```

首次运行初始化

```shell
┌──(root㉿kali)-[~]
└─# xray
```

### 1.2  Windows

下载

```powershell
PS C:\Users\sec> Invoke-WebRequest -Uri "https://github.com/chaitin/xray/releases/download/1.9.11/xray_windows_amd64.exe.zip" -Proxy "http://127.0.0.1:10809" -OutFile "xray_linux_amd64.zip"
```

windows 中使用 start.bat 脚本

```powershell
@echo off
set "XRAY_DIR=%~dp0"
set "PATH=%XRAY_DIR%;%PATH%"
start powershell -NoExit -Command "& { xray }"
```

## 2 初始化

生成证书

```shell
┌──(root㉿kali)-[~]
└─# xray genca
```

```
/root/tools/xray/ca.crt
```

打开安全设置

![打开安全设置](./../../../../images/xray/%E6%89%93%E5%BC%80%E5%AE%89%E5%85%A8%E8%AE%BE%E7%BD%AE.png)

管理证书

![管理证书](./../../../../images/xray/%E7%AE%A1%E7%90%86%E8%AF%81%E4%B9%A6.png)

导入证书

![导入证书](./../../../../images/xray/%E5%AF%BC%E5%85%A5%E8%AF%81%E4%B9%A6.png)

信任该证书

![信任该证书](./../../../../images/xray/%E4%BF%A1%E4%BB%BB%E8%AF%A5%E8%AF%81%E4%B9%A6.png)

重新加载

```shell
┌──(root㉿a-kali-23)-[~]
└─# xray
```

删除不允许访问的名单

```shell
┌──(root㉿a-kali-23)-[~]
└─# vim /root/tools/xray/config.yaml
```

```yaml
150    hostname_allowed: []                # 允许访问的 Hostname，支持格式如 t.com、*.t.com、1.1.1.1、1.1.1.1/24、1.1-4.1.1-8
151    hostname_disallowed:                # 不允许访问的 Hostname，支持格式如 t.com、*.t.com、1.1.1.1、1.1.1.1/24、1.1-4.1.1-8
152    - '*google*'
153    - '*github*'
154    - '*.gov.cn'
155    - '*.xray.cool'
```

> 删除 `*.edu.cn` ， `*chaitin*` 

## 3 使用

查看帮助

```shell
┌──(root㉿a-kali-23)-[~]
└─# xray -h
```

### 2.1 主动扫描

访问靶场

> http://a-centos7-6.local/dvwa/login.php
>
> 用户名	admin
>
> 密码	password

登录后使用 xray 对靶场进行主动扫描

```shell
┌──(root㉿a-kali-23)-[~]
└─# xray webscan --basic-crawler http://a-centos7-6.local/dvwa/ --html-output dvwa.html
```

扫描报告会存放在安装目录中

```
/root/tools/xray/dvwa.html
```

### 2.2 被动扫描

在 xray 配置被动扫描

```shell
┌──(root㉿kali)-[~]
└─# xray webscan --listen 192.168.1.14:7777 --html-output scan.html
```

配置 xray 代理启动 chrome

```shell
┌──(root㉿kali)-[~]
└─# google-chrome --proxy-server=http://192.168.1.14:7777
```

访问靶场

> http://a-centos7-6.local/pikachu/

此时浏览网页，xray 会在后台自动扫描

![此时浏览网页，xray 会在后台自动扫描](./../../../../images/xray/%E6%AD%A4%E6%97%B6%E6%B5%8F%E8%A7%88%E7%BD%91%E9%A1%B5%EF%BC%8Cxray%20%E4%BC%9A%E5%9C%A8%E5%90%8E%E5%8F%B0%E8%87%AA%E5%8A%A8%E6%89%AB%E6%8F%8F.png)

### 2.3 多重代理

**burp+xray**

在 xray 配置被动扫描

```shell
┌──(root㉿a-kali-23)-[~]
└─# xray webscan --listen 192.168.1.14:7777 --html-output scan.html
```

开启 burp

```shell
┌──(root㉿a-kali-23)-[~]
└─# burp
```

在 burp 配置 xray 代理

```
http://192.168.1.14:7777
```

![在 burp 配置 xray 代理](./../../../../images/xray/%E5%9C%A8%20burp%20%E9%85%8D%E7%BD%AE%20xray%20%E4%BB%A3%E7%90%86.png)

配置 burp 代理启动 chrome

```shell
┌──(root㉿kali)-[~]
└─# google-chrome --proxy-server=http://127.0.0.1:8080
```

此时会在 burp 和 xray 同时捕获到数据包

![此时会在 burp 和 xray 同时捕获到数据包](./../../../../images/xray/%E6%AD%A4%E6%97%B6%E4%BC%9A%E5%9C%A8%20burp%20%E5%92%8C%20xray%20%E5%90%8C%E6%97%B6%E6%8D%95%E8%8E%B7%E5%88%B0%E6%95%B0%E6%8D%AE%E5%8C%85.png)

**rad+xray**

在 xray 配置被动扫描

```shell
┌──(root㉿a-kali-23)-[~]
└─# xray webscan --listen 127.0.0.1:7777 --html-output scan.html
```

配置 xray 代理启动 rad

```shell
┌──(root㉿a-kali-23)-[~]
└─# rad -t http://a-centos7-6.local/pikachu/ --http-proxy http://127.0.0.1:7777
```

**rad+burp+xray**

在 xray 配置被动扫描

```shell
┌──(root㉿a-kali-23)-[~]
└─# xray webscan --listen 127.0.0.1:7777 --html-output scan.html
```

开启 burp

```shell
┌──(root㉿a-kali-23)-[~]
└─# burp
```

在 burp 配置 xray 代理

```
http://127.0.0.1:7777
```

![在 burp 配置 xray 代理](./../../../../images/xray/%E5%9C%A8%20burp%20%E9%85%8D%E7%BD%AE%20xray%20%E4%BB%A3%E7%90%86.png)

配置 burp 代理启动 rad

```shell
┌──(root㉿a-kali-23)-[~]
└─# rad -t http://a-centos7-6.local/pikachu/ --http-proxy http://127.0.0.1:8080
```

---

参考链接

- [xray](https://github.com/chaitin/xray)
