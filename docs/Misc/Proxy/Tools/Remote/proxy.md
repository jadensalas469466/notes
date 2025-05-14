用于配置全局代理.

## 1. install

将脚本下载到本地

```
mkdir -p /root/proxy && cd /root/proxy && \
curl -LO https://raw.githubusercontent.com/jadensalas469466/tools/refs/heads/main/other/proxy.sh
```

写入环境变量

```
echo "source /root/proxy/proxy.sh" >> ~/.zshrc && source ~/.zshrc
```

## 2. use

配置代理

```
proxy <ip:port>
```

取消代理

```
proxy
```

---

Refrences

- [proxy](https://github.com/jadensalas469466/tools/blob/main/other/proxy.sh)

