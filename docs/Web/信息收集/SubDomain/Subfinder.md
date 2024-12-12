## 1 部署

安装

```shell
root@debian:~# apt install -y subfinder
```

## 2 初始化

配置 API

```shell
root@debian:~# vim /root/.config/subfinder/provider-config.yaml
```

## 3 使用

经典扫描

```shell
root@debian:~# subfinder -d example.com -o subDomains.txt
```

扫描存活的 Host 并显示 IP

```shell
root@debian:~# subfinder -d example.com -active -ip -o HostIP.txt
```

