一个用于创建和管理容器的工具.

## 1. 安装

安装

```
┌──(root@debian)-[~]
└─# apt install -y docker.io \
&& curl -LO https://raw.githubusercontent.com/jadensalas469466/tools/refs/heads/main/other/docker-compose.sh \
&& bash docker-compose.sh && rm -rf docker-compose.sh
```

## 2. 初始化

配置开机自启

```
┌──(root@debian)-[~]
└─# systemctl enable --now docker.service
```

配置代理

```
┌──(root@debian)-[~]
└─# mkdir -p /etc/systemd/system/docker.service.d \
&& vim /etc/systemd/system/docker.service.d/http-proxy.conf
```

```
[Service]
Environment="HTTP_PROXY=http://192.168.1.201:10808"
Environment="HTTPS_PROXY=http://192.168.1.201:10808"
Environment="NO_PROXY=localhost,127.0.0.1,192.168.1.0/24"
```

重启 Docker 加载配置

```
┌──(root@debian)-[~]
└─# systemctl daemon-reload && systemctl restart docker.service
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
