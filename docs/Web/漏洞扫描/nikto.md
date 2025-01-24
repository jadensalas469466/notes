Web 漏洞扫描工具.

## 1. 安装

安装

```
apt install -y nikto
```

## 2. 使用

经典扫描

```
nikto -h http://example.com -o fileName.htm -Format htm
```

扫描 HTTPS 网站

```
nikto -h https://example.com -p 443 -ssl -o fileName.htm -Format htm
```

---

参考链接

- [nikto](https://www.kali.org/tools/nikto/)
