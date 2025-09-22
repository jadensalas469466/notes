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

---

References

- [frp](https://github.com/fatedier/frp)