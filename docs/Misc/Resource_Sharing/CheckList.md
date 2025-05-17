## 1. 目标确认

### 1.1. 公告审阅

在公告中查看目标的收录范围, 和测试限制

```
中国移动所有产品和服务
```

## 1.2. Whois

查询域名, 获取注册信息

```
whois 10086.cn
```

```
中国移动通信有限公司
```

### 1.3. ICP 备案查询

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

> 即使主域名无法访, 也需要保存, 后期可收集子域名

## 2. 信息收集

某些网站会收集在[站点导航](https://www.10086.cn/web_notice/navigation/)中, 直接访问即可

subfinder

```
subfinder -d 10086.cn -o subfinder_10086.cn.txt
```

Shodan

```
hostname:10086.cn http.status:200 country:CN ssl.cert.expired:true
```

HUNTER

```
domain.suffix="10086.cn"&&header.status_code="200"&&ip.country="CN"&&cert.is_trust=true
```

FOFA

```
domain="10086.cn" && status_code="200" && country="CN" && cert.is_valid=true
```

QUAKE

```
domain:"10086.cn" AND status_code:"200" AND country:"CN" AND browser_trusted:true
```

ZoomEye

```
domain="10086.cn" && http.header.status_code="200" && country="CN"
```

### 2.1 FingerPrints

## 3. 关系梳理

在 Open Multiple URLs 中访问每个站点, 保留有业务的站点;

手工访问每个业务板块, 使用 Xmind 绘制思维导图;

手工测试每个功能点, 使用 Visio 绘制流程图.

## 4. 信息泄露

### 4.1. 扫描仓库

Scan a repo for only verified secrets

```
trufflehog git https://github.com/trufflesecurity/test_keys --results=verified,unknown
```

### 4.2. AccessKey 泄露

