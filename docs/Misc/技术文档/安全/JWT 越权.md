 JWT 是一种凭证，可以授予对资源的访问权限。

## 1 分析

通常以 `eyJ` 开头的一段 Base64 编码字符串就是 JWT

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c # 示例
Header.Payload.Signature                                            # 示例
```

在请求包中的常见形式

```
auth: Header.Payload.Signature
Authorization: Bearer Header.Payload.Signature
```

Header

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9 # 编码
{"alg":"HS256","typ":"JWT"}          # 解码
```

Payload

```
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ # 编码
{"sub":"1234567890","name":"John Doe","iat":1516239022}                    # 解码
```

Signature

```
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c             # 编码
{"sub":"1234567890","name":"John Doe","iat":1516239022} # 解码
```

## 2 越权

可通过修改签名部分的用户名越权

```
"name":"John Doe"
"name":"Henrik White"
```

若失败可先将 HEADER 算法改为 `none` 再次尝试越权

```
"alg":"HS256"
"alg":"none"
```

