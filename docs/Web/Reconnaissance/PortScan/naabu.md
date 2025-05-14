快速的端口扫描工具.

## 1. 安装

安装

```
go install -v github.com/projectdiscovery/naabu/v2/cmd/naabu@latest
```

## 2. 使用

扫描 Top 1000 端口开放的目标

```
root@debian:~# naabu -l fileName.txt -tp 1000 -o fileName.txt
```

---

Refrences

- [naabu](https://www.kali.org/tools/naabu/)
