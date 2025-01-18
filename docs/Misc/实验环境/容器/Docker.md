一个用于创建和管理容器的工具.

## 1. 安装

安装

```
curl -fsSL https://get.docker.com -o get-docker.sh \
&& sh ./get-docker.sh && rm -rf ./get-docker.sh
```

## 2. 初始化

配置代理

```
mkdir -p /etc/systemd/system/docker.service.d \
&& nano /etc/systemd/system/docker.service.d/http-proxy.conf
```

```
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:10808"
Environment="HTTPS_PROXY=http://127.0.0.1:10808"
Environment="NO_PROXY=localhost,127.0.0.1,192.168.1.0/24"
```

重启 Docker 加载配置

```
systemctl daemon-reload && systemctl restart docker.service
```

## 3 使用

拉取镜像

```
docker pull <URL>
```

---

参考链接

- [Docker](https://www.docker.com/)
- [Docker Documentation](https://docs.docker.com/)
