Docker helps developers build, share, run, and verify applications anywhere — without tedious environment configuration or management.

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ curl -fsSL https://get.docker.com | sh
```

## 2. Init

配置代理

```
┌──(sec@debian)-[~]
└─$ sudo mkdir -p /etc/systemd/system/docker.service.d \
&& sudo nano /etc/systemd/system/docker.service.d/http-proxy.conf
```

```
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:10808"
Environment="HTTPS_PROXY=http://127.0.0.1:10808"
Environment="NO_PROXY=localhost,127.0.0.1,192.168.0.0/16,::1"
```

重启 Docker 加载配置

```
┌──(sec@debian)-[~]
└─$ sudo systemctl daemon-reload && sudo systemctl restart docker.service
```

## 3. Usage

拉取镜像

```
┌──(sec@debian)-[~]
└─$ docker pull <URL>
```

---

Refrences

- [Docker](https://www.docker.com/)
- [Docker Documentation](https://docs.docker.com/)
