监听端口

```shell
┌──(root㉿kali)-[~]
└─# nc -nvlp [port]
```

先半交互 Shell

```shell
root@debian:~# python -c 'import pty;pty.spawn("/bin/bash")'
```

再全交互 Shell

```shell
root@debian:~# stty raw -echo;fg;reset
```

