用于配置系统代理.

## 1. 安装

将脚本下载到本地

```
mkdir /root/tools/apps/proxy \
&& curl -L https://raw.githubusercontent.com/jadensalas469466/tools/refs/heads/main/other/proxy.sh -o /root/tools/apps/proxy/proxy.sh
```

创建链接

```
chmod +x /root/tools/apps/proxy/proxy.sh \
&& ln -s /root/tools/apps/proxy/proxy.sh /usr/local/bin/proxy
```

## 2. 使用

配置代理

```
proxy <ip:port>
```

取消代理

```
proxy
```

---

参考链接

- [proxy](https://github.com/jadensalas469466/tools/blob/main/other/proxy.sh)

