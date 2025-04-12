ccessKey ID 和 AccessKey Secret 是调用云服务器 API 时用于完成身份验证的凭证,

 AccessKey 泄露会对该账号下所有资源的安全带来威胁.

HUNTER

```
domain.suffix="example.com" && (web.body="AccessKey ID" || web.body="AccessKey Secret")
```

FOFA

```
domain="example.com" && (body="AccessKey ID" || body="AccessKey Secret")
```

Google

```
site:"example.com" "AccessKey ID" OR "AccessKey Secret"
```

Search Public Code

```
"example.com" AND ("AccessKey ID" OR "AccessKey Secret")
```

得到 AccessKey 后可使用 [OSSBrowser](https://help.aliyun.com/zh/oss/developer-reference/ossbrowser-2-0-overview?spm=a2c4g.11186623.help-menu-31815.d_3_4_3_0.29b73cca99hU99) 登录

---

参考链接

- [云业务 AccessKey 标识特征整理](https://wiki.teamssix.com/cloudservice/more/)
- [云上攻防 | 记一次AccessKey值泄露的挖掘和分析](https://rivers.chaitin.cn/blog/cqq5arp0lnec5jjugkqg)