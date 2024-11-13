一款用于分块传输绕过 WAF 的 Burp Suite 插件。

# 1 使用

查看扩展配置

![查看扩展配置](./../../../../../images/Chunked%20coding%20converter/%E6%9F%A5%E7%9C%8B%E6%89%A9%E5%B1%95%E9%85%8D%E7%BD%AE.png)

只开启代理即可

![只开启代理即可](./../../../../../images/Chunked%20coding%20converter/%E5%8F%AA%E5%BC%80%E5%90%AF%E4%BB%A3%E7%90%86%E5%8D%B3%E5%8F%AF.png)

> 其中分块大小表示将请求体数据每段大小，注释长度表示添加的数据大小
>
> Act on 表示这个扩展在哪里生效，若勾选代理，则是从代理发送的请求包自动进行分块处理

点击编码请求体

![点击编码请求体](./../../../../../images/Chunked%20coding%20converter/%E7%82%B9%E5%87%BB%E7%BC%96%E7%A0%81%E8%AF%B7%E6%B1%82%E4%BD%93.png)

发送请求数据包

![发送请求数据包](./../../../../../images/Chunked%20coding%20converter/%E5%8F%91%E9%80%81%E8%AF%B7%E6%B1%82%E6%95%B0%E6%8D%AE%E5%8C%85.png)

> 可以看到成功绕过
>
> 并且在请求体中进行了分块处理

**使用 sqlmap 利用分块传输饶过**

在 BurpSuite 添加一个可被 Kali 访问的代理

![在 BurpSuite 添加一个可被 Kali 访问的代理](./../../../../../images/Chunked%20coding%20converter/%E5%9C%A8%20BurpSuite%20%E6%B7%BB%E5%8A%A0%E4%B8%80%E4%B8%AA%E5%8F%AF%E8%A2%AB%20Kali%20%E8%AE%BF%E9%97%AE%E7%9A%84%E4%BB%A3%E7%90%86.png)

保存 BurpSuite 的请求数据包到 Kali 的 reg.txt

```http
POST /sqli-labs/Less-11/ HTTP/1.1
Host: 192.168.1.15
Content-Length: 30
Cache-Control: max-age=0
Origin: http://192.168.1.15
DNT: 1
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.1.15/sqli-labs/Less-11/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

uname=1&passwd=2&submit=Submit
```

> 交互栏的传输内容任意

在 sqlmap 指定请求文件和代理爆破

![在 sqlmap 指定请求文件和代理爆破](./../../../../../images/Chunked%20coding%20converter/%E5%9C%A8%20sqlmap%20%E6%8C%87%E5%AE%9A%E8%AF%B7%E6%B1%82%E6%96%87%E4%BB%B6%E5%92%8C%E4%BB%A3%E7%90%86%E7%88%86%E7%A0%B4.png)

> 可以看到经过扩展的请求体自动进行了分块处理

---

参考链接

- [Chunked coding converter](https://github.com/c0ny1/chunked-coding-converter)