Docker helps developers build, share, run, and verify applications anywhere — without tedious environment configuration or management.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ curl -fsSL https://get.docker.com | sh
```

## 2. Init

将当前用户追加到 `docker` 用户组

```
┌──(nemo@debian)-[~]
└─$ sudo usermod -aG docker $USER && newgrp docker
```

配置代理

```
┌──(nemo@debian)-[~]
└─$ sudo mkdir -p /etc/systemd/system/docker.service.d \
&& sudo tee /etc/systemd/system/docker.service.d/http-proxy.conf > /dev/null << 'EOF'
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:10808"
Environment="HTTPS_PROXY=http://127.0.0.1:10808"
Environment="NO_PROXY=localhost,127.0.0.1,192.168.0.0/16,::1"
EOF
```

重启 Docker 加载配置

```
┌──(nemo@debian)-[~]
└─$ sudo systemctl daemon-reload && sudo systemctl restart docker.service
```

## 3. Usage

拉取镜像

```
┌──(nemo@debian)-[~]
└─$ docker pull <URL>
```

---

References

- [Docker](https://www.docker.com/)

