超文本传输协议

| HTTP 字段      | 对应术语   | 说明                                                         |
| -------------- | ---------- | ------------------------------------------------------------ |
| Request        | 请求行     | HTTP 请求中的第一行，包含请求方法、URL 和协议版本            |
| Response       | 响应行     | HTTP 响应中的第一行，包含协议版本、状态码和状态消息          |
| User-Agent     | 用户代理   | 发起请求的客户端应用程序的标识符                             |
| Content-Length | 内容长度   | 请求或响应正文的长度（以字节为单位）                         |
| Content-Type   | 内容类型   | 请求或响应正文的 MIME 类型（如 text/html、application/json 等） |
| Host           | 主机       | 请求的目标主机（域名或 IP 地址）                             |
| Cookie         | Cookie     | 包含在请求或响应中的 HTTP Cookie                             |
| Set-Cookie     | 设置Cookie | 服务器发送给客户端的 HTTP Set-Cookie 头部，用于设置 Cookie   |
| Referer        | 引用来源   | 发起请求的页面的 URL（仅在请求中出现）                       |
| Location       | 重定向位置 | 服务器重定向响应中的新位置 URL（仅在响                       |

## 1 Get

```http
GET /pikachu/vul/ssrf/ssrf_curl.php?url=http://127.0.0.1/pikachu/vul/ssrf/ssrf_info/info1.php HTTP/1.1
Host: a-centos7-6.local


```

## 2 Post

```http
POST /pikachu/vul/burteforce/bf_form.php HTTP/1.1
Host: a-centos7-6.local
Content-Length: 48
Content-Type: application/x-www-form-urlencoded

username=admin123&password=admin456&submit=Login
```

## 3 响应状态码

HTTP 响应状态码用来表明特定 HTTP 请求是否成功完成。 响应被归为以下五大类：

> 1. [信息响应](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status#信息响应) (`100`–`199`)
> 2. [成功响应](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status#成功响应) (`200`–`299`)
> 3. [重定向消息](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status#重定向消息) (`300`–`399`)
> 4. [客户端错误响应](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status#客户端错误响应) (`400`–`499`)
> 5. [服务端错误响应](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status#服务端错误响应) (`500`–`599`)

---

参考链接

- [HTTP](https://developer.mozilla.org/zh-CN/docs/Web/HTTP)
