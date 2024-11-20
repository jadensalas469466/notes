一个用于创建和管理容器的工具。

## 1 部署

安装

```shell
root@server:~# apt install -y docker.io docker-compose
```

## 2 初始化

配置开机自启

```shell
root@server:~# systemctl enable --now docker.service
```

## 3 使用

通过 docker proxy 拉取镜像

```shell
root@server:~# docker pull dockerproxy.net/stilleshan/frpc:latest
```

配置代理

```shell
root@server:~# mkdir -p /etc/systemd/system/docker.service.d
```

```shell
root@server:~# vim /etc/systemd/system/docker.service.d/http-proxy.conf
```

```
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:10809"
Environment="HTTPS_PROXY=http://127.0.0.1:10809"
Environment="NO_PROXY=localhost,127.0.0.1"
```

重启 docker 加载配置

```shell
root@server:~# systemctl daemon-reload && systemctl restart docker.service
```

---

参考链接

- [docker](https://www.docker.com/)
- [docker proxy](https://dockerproxy.net/)
- [docker Documentation](https://docs.docker.com/)
