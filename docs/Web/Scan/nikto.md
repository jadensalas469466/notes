Nikto is a pluggable web server and CGI scanner written in Perl, using rfp’s LibWhisker to perform fast security or informational checks.

## 1. install

安装

```
apt install -y nikto
```

## 2. use

经典扫描

```
nikto -h http://example.com -o fileName.htm -Format htm
```

扫描 HTTPS 网站

```
nikto -h https://example.com -p 443 -ssl -o fileName.htm -Format htm
```

---

Refrences

- [nikto](https://www.kali.org/tools/nikto/)

