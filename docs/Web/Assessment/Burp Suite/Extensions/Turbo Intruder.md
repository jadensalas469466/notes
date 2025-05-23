一个用于并发的 Burp Suite Extensions.

## 1 使用

在请求包中添加 `%s` 后选择 `examples/race.py` 

![在请求包中添加 %s 后选择 examplesrace.py](./../../../../../images/Turbo%20Intruder/%E5%9C%A8%E8%AF%B7%E6%B1%82%E5%8C%85%E4%B8%AD%E6%B7%BB%E5%8A%A0%20%25s%20%E5%90%8E%E9%80%89%E6%8B%A9%20examplesrace.py.png)

设置并发 30 次

```
要保证 concurrentConnections=30 * requestsPerConnection=100 >= for i in range(30)
```

![设置并发 30 次](./../../../../../images/Turbo%20Intruder/%E8%AE%BE%E7%BD%AE%E5%B9%B6%E5%8F%91%2030%20%E6%AC%A1.png)

---

Refrences

- [Turbo Intruder](https://github.com/portswigger/turbo-intruder)

