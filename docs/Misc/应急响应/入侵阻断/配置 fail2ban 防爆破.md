---
layout:        post
title:        "配置 fail2ban 防爆破"
header-style:  text
catalog:       true
tags:
    - Misc
    - 应急响应
    - 入侵阻断

---

[fail2ban](https://github.com/fail2ban/fail2ban) 可以防止攻击者在短时间内对目标端口进行暴力破解

## 部署

安装

```shell
root@server:~# apt install -y fail2ban
```

## 初始化

修改配置文件

```shell
root@server:~# cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local && vim /etc/fail2ban/jail.local
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

```shell
root@server:~# systemctl enable --now fail2ban.service
```

## 使用

查看封禁的 IP

```shell
root@server:~# fail2ban-client status sshd | grep -A 5 "IP list"
```

移除封禁的 IP

```shell
root@server:~# fail2ban-client set sshd unbanip xxx.xxx.xxx.xxx
```

---

参考链接

- [fail2ban配置教程 有效防止服务器被暴力破解](https://www.wanpeng.life/1672.html)
