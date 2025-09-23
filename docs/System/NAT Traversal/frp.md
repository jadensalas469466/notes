A fast reverse proxy to help you expose a local server behind a NAT or firewall to the internet.

## 1. Install

```
curl -LO https://github.com/fatedier/frp/releases/download/v0.64.0/frp_0.64.0_linux_amd64.tar.gz
```

```
tar -xzvf ./frp_*_linux_amd64.tar.gz \
&& mv ./frp_*_linux_amd64 ~/.local/frp
```

```
ln -s ~/.local/frp/frps ~/.local/bin/frps \
&& ln -s ~/.local/frp/frpc ~/.local/bin/frpc
```

## 2. Init

```
cp ~/.local/frp/frpc.toml ~/.local/frp/frpc.toml.bak \
&& cat << 'EOF' > ~/.local/frp/frpc.toml
serverAddr = "1.1.1.1"
serverPort = 7000

[[proxies]]
name = "tcp"
type = "tcp"
localIP = "127.0.0.1"
localPort = 6000
remotePort = 6000
EOF
```

---

References

- [frp](https://github.com/fatedier/frp)