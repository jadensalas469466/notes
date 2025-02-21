## 1. [Discovering API documentation](https://portswigger.net/web-security/api-testing/lab-exploiting-api-endpoint-using-documentation)

通用思路:

- 跑路径
- FindSomething
- Burp 扫描仪
- JS 文件

### 1.1. 跑协议

修改邮箱后发现一个 API

![修改邮箱后发现一个 API](./../../../images/API%20testing/%E4%BF%AE%E6%94%B9%E9%82%AE%E7%AE%B1%E5%90%8E%E5%8F%91%E7%8E%B0%E4%B8%80%E4%B8%AA%20API.png)

删除请求体, 测试 API 可能使用的所有请求类型

```
DELETE 类型要手动测试, 否则会对目标造成不可逆的损害
```

![删除请求体, 测试 API 可能使用的所有请求类型](./../../../images/API%20testing/%E5%88%A0%E9%99%A4%E8%AF%B7%E6%B1%82%E4%BD%93,%20%E6%B5%8B%E8%AF%95%20API%20%E5%8F%AF%E8%83%BD%E4%BD%BF%E7%94%A8%E7%9A%84%E6%89%80%E6%9C%89%E8%AF%B7%E6%B1%82%E7%B1%BB%E5%9E%8B.png)

最后发现有一个 GET 类型的请求可访问, 且存在敏感信息泄露

![最后发现有一个 GET 类型的请求可访问, 且存在敏感信息泄露](./../../../images/API%20testing/%E6%9C%80%E5%90%8E%E5%8F%91%E7%8E%B0%E6%9C%89%E4%B8%80%E4%B8%AA%20GET%20%E7%B1%BB%E5%9E%8B%E7%9A%84%E8%AF%B7%E6%B1%82%E5%8F%AF%E8%AE%BF%E9%97%AE,%20%E4%B8%94%E5%AD%98%E5%9C%A8%E6%95%8F%E6%84%9F%E4%BF%A1%E6%81%AF%E6%B3%84%E9%9C%B2.png)

对这个 API 的每个字段进行增删改查 (删除字段时要将 `/` 视为一个字段) 最后发现存在 API 文档泄露

![对这个 API 的每个字段进行增删改查, 最后发现存在 API 文档泄露](./../../../images/API%20testing/%E5%AF%B9%E8%BF%99%E4%B8%AA%20API%20%E7%9A%84%E6%AF%8F%E4%B8%AA%E5%AD%97%E6%AE%B5%E8%BF%9B%E8%A1%8C%E5%A2%9E%E5%88%A0%E6%94%B9%E6%9F%A5,%20%E6%9C%80%E5%90%8E%E5%8F%91%E7%8E%B0%E5%AD%98%E5%9C%A8%20API%20%E6%96%87%E6%A1%A3%E6%B3%84%E9%9C%B2.png)

逐个测试 API 文档中的 API, 最后发现 `DELETE` 可利用

![逐个测试 API 文档中的 API, 最后发现 `DELETE` 可利用](./../../../images/API%20testing/%E9%80%90%E4%B8%AA%E6%B5%8B%E8%AF%95%20API%20%E6%96%87%E6%A1%A3%E4%B8%AD%E7%9A%84%20API,%20%E6%9C%80%E5%90%8E%E5%8F%91%E7%8E%B0%20%60DELETE%60%20%E5%8F%AF%E5%88%A9%E7%94%A8.png)

---

参考链接

- [HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

## 2. [Finding and exploiting an unused API endpoint](https://portswigger.net/web-security/api-testing/lab-exploiting-unused-api-endpoint)

发现一个用于控制价格的 API

![发现一个用于控制价格的 API](./../../../images/API%20testing/%E5%8F%91%E7%8E%B0%E4%B8%80%E4%B8%AA%E7%94%A8%E4%BA%8E%E6%8E%A7%E5%88%B6%E4%BB%B7%E6%A0%BC%E7%9A%84%20API.png)

在对请求方式进行爆破后发现返回包中存在提示

![在对请求方式进行爆破后发现返回包中存在提示](./../../../images/API%20testing/%E5%9C%A8%E5%AF%B9%E8%AF%B7%E6%B1%82%E6%96%B9%E5%BC%8F%E8%BF%9B%E8%A1%8C%E7%88%86%E7%A0%B4%E5%90%8E%E5%8F%91%E7%8E%B0%E8%BF%94%E5%9B%9E%E5%8C%85%E4%B8%AD%E5%AD%98%E5%9C%A8%E6%8F%90%E7%A4%BA.png)

尝试测试 PATCH 发现返回的是未授权

![尝试测试 PATCH 发现返回的是未授权](./../../../images/API%20testing/%E5%B0%9D%E8%AF%95%E6%B5%8B%E8%AF%95%20PATCH%20%E5%8F%91%E7%8E%B0%E8%BF%94%E5%9B%9E%E7%9A%84%E6%98%AF%E6%9C%AA%E6%8E%88%E6%9D%83.png)

登录后重新测试发现需要设置 `Content-Type`

![登录后重新测试发现需要设置 `Content-Type`](./../../../images/API%20testing/%E7%99%BB%E5%BD%95%E5%90%8E%E9%87%8D%E6%96%B0%E6%B5%8B%E8%AF%95%E5%8F%91%E7%8E%B0%E9%9C%80%E8%A6%81%E8%AE%BE%E7%BD%AE%20%60Content-Type%60.png)

设置 `Content-Type` 后重新发送发现报错, 猜测可能是需要添加 JSON 格式的请求体

![设置 `Content-Type` 后重新发送发现报错](./../../../images/API%20testing/%E8%AE%BE%E7%BD%AE%20%60Content-Type%60%20%E5%90%8E%E9%87%8D%E6%96%B0%E5%8F%91%E9%80%81%E5%8F%91%E7%8E%B0%E6%8A%A5%E9%94%99.png)

添加 JSON 格式后发现缺少字段 `price` 

![添加 JSON 格式后发现缺少字段 `price` ](./../../../images/API%20testing/%E6%B7%BB%E5%8A%A0%20JSON%20%E6%A0%BC%E5%BC%8F%E5%90%8E%E5%8F%91%E7%8E%B0%E7%BC%BA%E5%B0%91%E5%AD%97%E6%AE%B5%20%60price%60%20.png)

尝试添加字段后成功修改价格

![尝试添加字段后成功修改价格](./../../../images/API%20testing/%E5%B0%9D%E8%AF%95%E6%B7%BB%E5%8A%A0%E5%AD%97%E6%AE%B5%E5%90%8E%E6%88%90%E5%8A%9F%E4%BF%AE%E6%94%B9%E4%BB%B7%E6%A0%BC.png)
