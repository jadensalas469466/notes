用于配置系统代理.

## 1. 安装

将脚本下载到本地

```
mkdir -p /root/proxy && curl -L https://raw.githubusercontent.com/jadensalas469466/tools/refs/heads/main/other/proxy.sh -o /root/proxy/proxy.sh
```

创建链接

```
chmod +x /root/proxy/proxy.sh \
&& ln -s /root/proxy/proxy.sh /usr/local/bin/proxy
```

## 2. 使用

配置代理

```
source proxy <ip:port>
```

取消代理

```
source proxy
```

---

Refrences

- [proxy](https://github.com/jadensalas469466/tools/blob/main/other/proxy.sh)

