The web application accepts a user-controlled input that specifies a link to an external site, and uses that link in a redirect.

目标网站存在一个 URL 跳转, 访问会跳转到 `http://test.com`

```
http://example.com?url=http://test.com
```

修改 URL 为 `http://evil.com` , 则会跳转到 `http://evil.com` 

```
http://example.com?url=http://evil.com
```

Common Query Parameters

```
u
r
url
redirect
redirectUrl
callback
checkout_url
continue
return_url
toUrl
ReturnUrl
fromUrl
redUrl
request
redirect_to
redirect_url
jump
jump_to
target
to
goto
link
linkto
domain
oauth_callback
```

---

Refrences

- [CWE-601: URL Redirection to Untrusted Site ('Open Redirect')](https://cwe.mitre.org/data/definitions/601.html)
- [Open URL Redirect](https://swisskyrepo.github.io/PayloadsAllTheThings/Open%20Redirect/)
- [URL Redirection to Untrusted Site ('Open Redirect')](https://hackerone.com/hacktivity/cwe_discovery?id=cwe-601)
- [URL跳转](https://wy.zone.ci/bugstypes_list.php?bugtype=URL%E8%B7%B3%E8%BD%AC)

