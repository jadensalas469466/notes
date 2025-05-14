加密网站管理客户端。

## 1 安装

下载

```shell
┌──(root㉿kali)-[~]
└─# wget https://mirror.ghproxy.com/https://github.com/rebeyond/Behinder/releases/download/Behinder_v4.1%E3%80%90t00ls%E4%B8%93%E7%89%88%E3%80%91/Behinder_v4.1.t00ls.zip
```

解压

```shell
┌──(root㉿kali)-[~]
└─# unzip Behinder_v4.1.t00ls.zip -d /root/tools/behinder && rm -rf /root/Behinder_v4.1.t00ls.zip
```

编写脚本

```shell
┌──(root㉿kali)-[~]
└─# vim /root/tools/behinder/behinder.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 修改 jre 为 /usr/local/jdk1.8.0_202/bin/java
nohup sudo update-alternatives --set java /usr/local/jdk1.8.0_202/bin/java >/dev/null 2>&1 &

# 运行 behinder
nohup sudo java -jar Behinder.jar "$@" >/dev/null 2>&1 &
```

创建链接

```shell
┌──(root㉿kali)-[~]
└─# chmod +x /root/tools/behinder/behinder.sh && ln -s /root/tools/behinder/behinder.sh /usr/local/bin/behinder
```

## 2 使用

运行

```shell
┌──(root㉿kali)-[~]
└─# behinder
```

**生成木马**

> 所有生成的木马默认密码都是 rebeyond 

将默认加密类型的木马上传到目标

```shell
┌──(root㉿kali)-[~]
└─# ls /root/tools/behinder/server/     
shell.ashx  shell.asp  shell.aspx  shell_java9.jsp  shell.jsp  shell.jspx  shell.php  shell_uni.jsp
```

或者生成自定义类型的木马上传到目标

![或者生成自定义类型的木马上传到目标](./../../../images/Behinder/%E6%88%96%E8%80%85%E7%94%9F%E6%88%90%E8%87%AA%E5%AE%9A%E4%B9%89%E7%B1%BB%E5%9E%8B%E7%9A%84%E6%9C%A8%E9%A9%AC%E4%B8%8A%E4%BC%A0%E5%88%B0%E7%9B%AE%E6%A0%87.png)

```shell
┌──(root㉿kali)-[~]
└─# ls /root/tools/behinder/server/default_aes
shell.ashx  shell.aspx  shell.jsp  shell.php
```

> default_aes 为传输协议名

新增 Shell 

![新增 Shell](./../../../images/Behinder/%E6%96%B0%E5%A2%9E%20Shell.png)

查看 Shell 

![查看 Shell](./../../../images/Behinder/%E6%9F%A5%E7%9C%8B%20Shell.png)

---

Refrences

- [Behinder](https://github.com/rebeyond/Behinder)