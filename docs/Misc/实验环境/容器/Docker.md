一个用于创建和管理容器的工具.

## 1. 安装

安装

```
┌──(root@debian)-[~]
└─# apt install -y docker.io \
&& DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker} \
&& mkdir -p $DOCKER_CONFIG/cli-plugins \
&& curl -SL https://github.com/docker/compose/releases/download/v2.32.0/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose \
&& chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose
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
Environment="HTTP_PROXY=http://192.168.1.201:10809"
Environment="HTTPS_PROXY=http://192.168.1.201:10809"
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
