Apache Shiro™ is a powerful and easy-to-use Java security framework that performs authentication, authorization, cryptography, and session management. With Shiro’s easy-to-understand API, you can quickly and easily secure any application – from the smallest mobile applications to the largest web and enterprise applications.

## 1. Fingerprint

HaE

```
(=deleteMe|rememberMe=)
```

在 login/logout 时, 响应包会返回

```
Set-Cookie: rememberMe=deleteMe
```

Login Page 1

![Login Page 1](./../../../../images/Shiro/Login%20Page%201.png)

Login Page 2

![Login Page 2](./../../../../images/Shiro/Login%20Page%202.png)

Login Page 3

![Login Page 3](./../../../../images/Shiro/Login%20Page%203.png)

## 2. Nday

### [2.1. CVE-2016-4437](https://hackerone.com/hacktivity/cve_discovery?id=CVE-2016-4437)

版本

```
Shiro < 1.2.5
```

靶场

```
vulfocus/shiro-cve_2016_4437:latest
```

工具

- [ShiroAttack2](https://github.com/SummerSec/ShiroAttack2)
- [ShiroAttack2_Pro](https://github.com/Chave0v0/ShiroAttack2_Pro)

### 2.1.1. PoC

爆破密钥 (AES-CBC, Shiro > 1.4.1)

![爆破密钥 (AES-CBC, Shiro  1.4.1)](./../../../../images/Shiro/%E7%88%86%E7%A0%B4%E5%AF%86%E9%92%A5%20(AES-CBC,%20Shiro%20%201.4.1).png)

爆破密钥 (AES-GCM, Shiro < 1.4.2)

![爆破密钥 (AES-GCM, Shiro  1.4.2)](./../../../../images/Shiro/%E7%88%86%E7%A0%B4%E5%AF%86%E9%92%A5%20(AES-GCM,%20Shiro%20%201.4.2).png)

某些情况下需要修改为目标网站自定义的关键字

```
Set-Cookie: sec-cms-r=deleteMe
```

![某些情况下需要修改为目标网站自定义的关键字](./../../../../images/Shiro/%E6%9F%90%E4%BA%9B%E6%83%85%E5%86%B5%E4%B8%8B%E9%9C%80%E8%A6%81%E4%BF%AE%E6%94%B9%E4%B8%BA%E7%9B%AE%E6%A0%87%E7%BD%91%E7%AB%99%E8%87%AA%E5%AE%9A%E4%B9%89%E7%9A%84%E5%85%B3%E9%94%AE%E5%AD%97.png)

### 2.2.2. Exploit

爆破利用链及回显

![爆破利用链及回显](./../../../../images/Shiro/%E7%88%86%E7%A0%B4%E5%88%A9%E7%94%A8%E9%93%BE%E5%8F%8A%E5%9B%9E%E6%98%BE.png)

命令执行

![命令执行](./../../../../images/Shiro/%E5%91%BD%E4%BB%A4%E6%89%A7%E8%A1%8C.png)

### [2.2. CVE-2019-12422](https://hackerone.com/hacktivity/cve_discovery?id=CVE-2019-12422)

```
Shiro < 1.4.2
```

```
vulfocus/shiro-721:latest
```



---

References

- [Shiro](https://shiro.apache.org/)
- [shiro框架漏洞学习](https://www.bilibili.com/video/BV1pRurzFE5W/?spm_id_from=333.1387.favlist.content.click&vd_source=2dcc7806c9580af60063ca1edb63852d)

