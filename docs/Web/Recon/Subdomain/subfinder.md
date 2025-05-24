Fast passive subdomain enumeration tool.

## 1. install

安装

```
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
```

## 2. use

经典扫描

```
subfinder -d example.com -o subfinder_example.com.txt
```

扫描存活的 Host 并显示 IP

```
subfinder -d example.com -active -ip -o subfinder_example.com_active_ip.txt
```

查看 API 配置

```
subfinder -ls
```

配置 API

```
vim /root/.config/subfinder/provider-config.yaml
```

---

Refrences

- [subfinder](https://github.com/projectdiscovery/subfinder)

