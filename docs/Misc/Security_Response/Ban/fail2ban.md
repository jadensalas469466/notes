可以防止攻击者在短时间内对目标端口进行暴力破解.

## 1. install

安装

```
apt install -y fail2ban
```

## 2. init

修改配置文件

```
cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local && nano /etc/fail2ban/jail.local
```

```
274 [sshd]
280 enabled  = true
281 port     = ssh
282 logpath = %(sshd_log)s
283 backend = %(sshd_backend)s
284 filter = sshd
285 action = iptables[name=SSH,port=ssh,protocol=tcp] 
286 bantime  = 86400
287 maxretry = 5
288 findtime = 300
```

运行 `fail2ban` 服务

```
systemctl enable --now fail2ban.service
```

## 3. use

查看封禁的 IP

```
fail2ban-client status sshd | grep -A 5 "IP list"
```

移除封禁的 IP

```
fail2ban-client set sshd unbanip [ban_ip]
```

---

Refrences

- [fail2ban](https://github.com/fail2ban/fail2ban)
- [fail2ban配置教程 有效防止服务器被暴力破解](https://www.wanpeng.life/1672.html)
