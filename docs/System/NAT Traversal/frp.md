A fast reverse proxy to help you expose a local server behind a NAT or firewall to the internet.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ curl -fsSL https://github.com/jadensalas469466/script/raw/main/frp_install.sh | bash
```

## 2. Init

### 2.1. Server

开机自启

```
┌──(nemo@debian)-[~]
└─$ sudo systemctl enable --now frps.service
```

开放端口用于建立通信和转发流量

```
┌──(nemo@debian)-[~]
└─$ sudo ufw allow 7000 && sudo ufw allow 6000
```

### 2.2. Client

修改配置文件

```
┌──(nemo@debian)-[~]
└─$ nano ~/.frp/frpc.toml
```

```
serverAddr = "evil.com"
serverPort = 7000
transport.tcpMux = true
transport.tls.enable = true
auth.tokenSource.type = "file"
auth.tokenSource.file.path = "/home/nemo/.frp/frp_token"

[[proxies]]
name = "tcp"
type = "tcp"
localIP = "127.0.0.1"
localPort = 6000
remotePort = 6000
```

修改为与 Server 相同的 Token

```
┌──(nemo@debian)-[~]
└─$ nano ~/.frp/frp_token
```

## 3. Usage

运行 Client

```
┌──(nemo@debian)-[~]
└─$ nohup frpc -c ~/.frp/frpc.toml > ~/frpc-nohup.log 2>&1 &
echo $! > ~/frpc-pid.log
```

> 此时发往 `evil.com:6000` 的流量会转发到 `127.0.0.1:6000` 

---

References

- [frp](https://github.com/fatedier/frp)

