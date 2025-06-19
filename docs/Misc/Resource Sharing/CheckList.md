## 1. Target

### 1.1. Notice

在公告中查看目标的收录范围, 和测试限制

```
中国移动所有产品和服务
```

### 1.2. ICP

[ICP/IP地址/域名信息备案管理系统](https://beian.miit.gov.cn/)

通过主办单位名称, 备案号, 域名互相反查

```
中国移动通信有限公司
京ICP备05002571号

10086.cn
cmccb2b.com
monternet.com
chinamobile.com
warmchina121.com
```

> 即使主域名无法访问, 也需要保存, 后期可收集子域名

## 2. Recon

某些网站会收集在 [站点导航](https://www.10086.cn/web_notice/navigation/) 中, 直接访问即可

### 2.1. Subdomain

FOFA

```
fofa查询 domain="10086.cn" && status_code="200" && country="CN" && cert.is_valid=true size=10000
```

## 3. 信息泄露

### 3.1. AccessKey 泄露

## 4. 手工测试

手工访问每个业务板块, 使用 Xmind 绘制思维导图;

手工测试每个功能点, 使用 Visio 绘制流程图.
