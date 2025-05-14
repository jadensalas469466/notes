## 1. 安装

安装

```
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
```

## 2. 初始化

初始化运行

```
subfinder -ls
```

配置 API

```
vim /root/.config/subfinder/provider-config.yaml
```

## 3. 使用

经典扫描

```
root@debian:~# subfinder -d example.com -o subDomains.txt
```

扫描存活的 Host 并显示 IP

```
root@debian:~# subfinder -d example.com -active -ip -o HostIP.txt
```

---

Refrences

- [subfinder](https://www.kali.org/tools/subfinder/)

