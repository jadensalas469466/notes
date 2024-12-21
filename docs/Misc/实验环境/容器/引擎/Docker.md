一个用于创建和管理容器的工具.

## 1 安装

安装

```shell
root@debian:~# apt install -y docker.io docker-compose
```

## 2 初始化

配置开机自启

```shell
root@debian:~# systemctl enable --now docker.service
```

## 3 使用

### 3.1 配置

配置代理

```shell
root@debian:~# mkdir -p /etc/systemd/system/docker.service.d && vim /etc/systemd/system/docker.service.d/http-proxy.conf
```

```
[Service]
Environment="HTTP_PROXY=http://192.168.1.201:10809"
Environment="HTTPS_PROXY=http://192.168.1.201:10809"
Environment="NO_PROXY=localhost,127.0.0.1,192.168.1.0/24"
```

重启 Docker 加载配置

```shell
root@debian:~# systemctl daemon-reload && systemctl restart docker.service
```

### 3.2 拉取

通过 docker proxy 拉取镜像

```shell
root@debian:~# docker pull dockerproxy.net/stilleshan/frpc:latest
```

---

参考链接

- [docker](https://www.docker.com/)
- [docker proxy](https://dockerproxy.net/)
- [docker Documentation](https://docs.docker.com/)
