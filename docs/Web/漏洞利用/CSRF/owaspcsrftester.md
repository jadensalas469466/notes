CSRF 自动生成。

运行 csrftester

![运行 csrftester](./../../../../images/owaspcsrftester/%E8%BF%90%E8%A1%8C%20csrftester.png)

开启录制

![开启录制](./../../../../images/owaspcsrftester/%E5%BC%80%E5%90%AF%E5%BD%95%E5%88%B6.png)

将流量转发到 csrftester 

> 127.0.0.1:8008

![将流量转发到 csrftester](./../../../../images/owaspcsrftester/%E5%B0%86%E6%B5%81%E9%87%8F%E8%BD%AC%E5%8F%91%E5%88%B0%20csrftester.png)

访问

> http://centos.local/dvwa/vulnerabilities/xss_s/

在 low 级别下提交留言

![在 low 级别下提交留言](./../../../../images/owaspcsrftester/%E5%9C%A8%20low%20%E7%BA%A7%E5%88%AB%E4%B8%8B%E6%8F%90%E4%BA%A4%E7%95%99%E8%A8%80.png)

停止录制

![停止录制](./../../../../images/owaspcsrftester/%E5%81%9C%E6%AD%A2%E5%BD%95%E5%88%B6.png)

在 csrftester 中找到对应的提交请求

> 一般为最后的 post

修改表单内容

> hello 123
>
> world 123

![修改表单内容](./../../../../images/owaspcsrftester/%E4%BF%AE%E6%94%B9%E8%A1%A8%E5%8D%95%E5%86%85%E5%AE%B9.png)

生成 html 文件到桌面

> 取消勾选 Display in Browser 

![生成 html 文件到桌面](./../../../../images/owaspcsrftester/%E7%94%9F%E6%88%90%20html%20%E6%96%87%E4%BB%B6%E5%88%B0%E6%A1%8C%E9%9D%A2.png)

运行这个 html 文件

![运行这个 html 文件](./../../../../images/owaspcsrftester/%E8%BF%90%E8%A1%8C%E8%BF%99%E4%B8%AA%20html%20%E6%96%87%E4%BB%B6.png)

> 成功修改

**burpsuite**

也可以使用 burpsuite 拦截正常请求生成 html 文件

![也可以使用 burpsuite 拦截正常请求生成 html 文件](./../../../../images/owaspcsrftester/%E4%B9%9F%E5%8F%AF%E4%BB%A5%E4%BD%BF%E7%94%A8%20burpsuite%20%E6%8B%A6%E6%88%AA%E6%AD%A3%E5%B8%B8%E8%AF%B7%E6%B1%82%E7%94%9F%E6%88%90%20html%20%E6%96%87%E4%BB%B6.png)

---

参考链接

- [owaspcsrftester](https://github.com/ot-jerry-welch/owaspcsrftester)