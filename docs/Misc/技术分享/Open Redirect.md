API 特征参数是 `url=` 
目标网站存在一个 URL 跳转, 访问会跳转到 `http://test.com`

```
https://example.com?url=http://test.com
```

修改 URL 为 `http://evil.com` , 则会跳转到 `http://evil.com` 

```
https://example.com?url=http://evil.com
```

绕过校验可利用 `@` , `/`, `\` 如:

访问 `https://example.com@evil.com` 

---

- [URL Redirection to Untrusted Site ('Open Redirect')](https://hackerone.com/hacktivity/cwe_discovery?id=cwe-601)
- [URL跳转](https://wy.zone.ci/bugstypes_list.php?bugtype=URL%E8%B7%B3%E8%BD%AC)

