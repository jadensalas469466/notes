## 1. 判断方法

### 1.1. 自动

```
FOFA
Wappalyzer
whatweb
dirsearch
```

### 1.2. 手动

```
View page source # 查看源码
https://example.com/<index.html> # 遍历敏感文件后缀
```

[泛微](https://www.weaver.com.cn/)

![Weaver](./../../../images/FingerPrints/Weaver.png)

[蓝凌](https://www.landray.com.cn/)

![Landray](./../../../images/FingerPrints/Landray.png)

[Spring](https://spring.io/)

![Spring](./../../../images/FingerPrints/Spring.png)

[ThinkPHP](https://www.thinkphp.cn/)

![ThinkPHP](./../../../images/FingerPrints/ThinkPHP.png)

## OSS

```
accessKey
OSSAccessKeyID
AccessKeyID
AccessKeySecret
```

## struts2

```
.action
.do
```

## shiro

```
rememberMe=
请记住我
```

## 敏感参数

```
inurl:email= | inurl:phone= inurl:password= | inurl:secret=
```

## 文件上传

```
"choose file" | "请上传文件"
```

## WordPress

```
root@kali:~# wpscan --url http://wordpress.local --enumerate p
```

