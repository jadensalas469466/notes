可以防止攻击者在短时间内对目标端口进行暴力破解.

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─# sudo apt install -y fail2ban
```

## 2. Init

修改配置文件

```
┌──(sec@debian)-[~]
└─# sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local \
&& sudo nano -l /etc/fail2ban/jail.local
```

```
274 [sshd]
280 enabled  = true
281 port     = ssh
282 logpath = %(sshd_log)s
283 backend = %(sshd_backend)s
filter = sshd
action = iptables[name=SSH,port=ssh,protocol=tcp] 
bantime  = 86400
maxretry = 5
findtime = 300
```

运行 `fail2ban` 服务

```
┌──(sec@debian)-[~]
└─# sudo systemctl enable --now fail2ban.service
```

## 3. Usage

查看封禁的 IP

```
┌──(sec@debian)-[~]
└─# fail2ban-client status sshd | grep -A 5 "IP list"
```

移除封禁的 IP

```
┌──(sec@debian)-[~]
└─# fail2ban-client set sshd unbanip [ban_ip]
```

---

Refrences

- [fail2ban](https://github.com/fail2ban/fail2ban)
- [fail2ban配置教程 有效防止服务器被暴力破解](https://www.wanpeng.life/1672.html)
