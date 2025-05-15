ffuf is a fast web fuzzer written in Go that allows typical directory discovery, virtual host discovery (without DNS records) and GET and POST parameter fuzzing.

## 1. install

安装

```
go install github.com/ffuf/ffuf/v2@latest
```

## 2. use

GET 扫描

```
ffuf -recursion-depth 3 \
-w /path/dict.txt:FUZZ \
-H "X-Originating-Ip: 127.0.0.1" \
-H "X-Remote-Ip: 127.0.0.1" \
-H "X-Forwarded-For: 127.0.0.1" \
-H "X-Remote-Addr: 127.0.0.1" \
-H "Cf-Connecting-Ip: 127.0.0.1" \
-u http://example.com/FUZZ -fs 0 \
-o results.json
```

---

Refrences

- [ffuf](https://www.kali.org/tools/ffuf/)