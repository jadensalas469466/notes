一款 Fuzzing 工具.

GET 扫描

```
┌──(root@debian)-[~]
└─# ffuf -recursion-depth 3 \
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

参考链接

- [ffuf](https://www.kali.org/tools/ffuf/)