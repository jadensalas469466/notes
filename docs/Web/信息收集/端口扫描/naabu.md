快速的端口扫描工具.

## 1. 部署

安装

```shell
root@debian:~# apt install -y naabu
```

## 2. 使用

扫描 Top 1000 端口并跳过 CND

```shell
root@debian:~# naabu -l fileName.txt -tp 1000 -ec -o fileName.txt
```

---

参考链接

- [naabu](https://www.kali.org/tools/naabu/)
