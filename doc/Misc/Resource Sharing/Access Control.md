AccessKey ID 和 AccessKey Secret 是调用云服务器 API 时用于完成身份验证的凭证,

AccessKey 泄露会对该账号下所有资源的安全带来威胁.

## 1. Web

Google

```
site:"example.com" ("AccessKeyID" OR "AccessKeySecret")
```

Search Public Code

```
"example.com" AND ("AccessKeyID" OR "AccessKeySecret")
```

HUNTER

```
domain.suffix="example.com"&&(web.body="AccessKeyID"||web.body="AccessKeySecret")
```

FOFA

```
domain="example.com" && (body="AccessKeyID" || body="AccessKeySecret")
```

QUAKE

```
domain:"example.com" AND (body="AccessKeyID" OR body:"AccessKeySecret")
```

ZoomEye

```
domain="example.com" && (http.body="AccessKeyID" || http.body="AccessKeySecret")
```

## 2. Repo

Search Public Code

```
"example.com" AND ("AccessKeyID" OR "AccessKeySecret")
```

Scan a repo for only verified secrets

```
trufflehog git https://github.com/trufflesecurity/test_keys --results=verified,unknown
```

得到 AccessKey 后可使用 [OSSBrowser](https://help.aliyun.com/zh/oss/developer-reference/ossbrowser-2-0-overview?spm=a2c4g.11186623.help-menu-31815.d_3_4_3_0.29b73cca99hU99) 登录

---

References

- [云业务 AccessKey 标识特征整理](https://wiki.teamssix.com/cloudservice/more/)
- [云上攻防 | 记一次AccessKey值泄露的挖掘和分析](https://rivers.chaitin.cn/blog/cqq5arp0lnec5jjugkqg)