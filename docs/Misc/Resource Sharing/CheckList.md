## 1. Target

### 1.1. Notice

在公告中查看目标的收录范围, 和测试限制

```
中国移动所有产品和服务
```

### 1.2. Whois

查询域名, 获取注册信息

```
┌──(sec@debian)-[~]
└─$ whois 10086.cn | tee -a whois.txt
```

```
中国移动通信有限公司
```

### 1.3. ICP

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

某些网站会收集在[站点导航](https://www.10086.cn/web_notice/navigation/)中, 直接访问即可

### 2.1. Subdomain

subfinder

```
┌──(sec@debian)-[~]
└─$ subfinder -d 10086.cn -o subfinder_10086.cn.txt
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

> 整合所有域名为 `subdomain.txt` 

### 2.2. DNS

```
┌──(sec@debian)-[~]
└─$ dig +short A 10086.cn | tee -a dig_ip.txt
```

> 使用 CDN 的 IP 仅保留主 IP

> 若在查询 A 记录时发现多个域名使用同一个 IP
>
> 手工访问 `subdomain.txt` 中的每个域名
>
> 若是同一站点仅保留一个即可, 如: `10086.cn` 和 `www.10086.cn` 

awk 去重

```
┌──(sec@debian)-[~]
└─$ awk '!seen[$0]++' dig_ip.txt > dig_ip.txt.tmp && mv dig_ip.txt.tmp dig_ip.txt
```

### 2.3. Port

naabu Top 100 端口扫描

```
┌──(sec@debian)-[~]
└─$ sudo naabu -l dig_ip.txt -tp 100 -Pn -o naabu_ip-port.txt
```

生成 `domain-port.txt` , 避免目标配置了仅从域名访问

```
┌──(sec@debian)-[~]
└─$ python3 ./domain-port.py
```

masscan 全端口扫描

```
┌──(sec@debian)-[~]
└─$ sudo masscan -p- -iL dig_ip.txt -oL masscan_port.txt
```

awk 提取出每个 IP 的开放端口

```
┌──(sec@debian)-[~]
└─$ awk '/^open/ {print $4, $3}' masscan_port.txt | sort -k1,1 -k2n | \
awk '{ips[$1] = (ips[$1] ? ips[$1]","$2 : $1":"$2)} END {for (ip in ips) print ips[ip]}' | tee awk_ip-port.txt
```

```
36.160.4.7:135,445,902
36.160.4.161:1026,5040,5357
```

nmap 指定端口识别

```
┌──(sec@debian)-[~]
└─$ sudo nmap -p 135,445,902,65535 -T4 -Pn -sV -O 36.160.4.7 -oN nmap_port.txt
```

> 指定一个不常用的端口用于系统检测如: `65535` 

### 2.4. HTTP Status

筛选出 Web 端口

```
┌──(sec@debian)-[~]
└─$ httpx -l domain-port.txt -o httpx_url.txt
```

> 若一个站点同时存在 HTTP 和 HTTPS, 仅保留 HTTP 即可

### 2.5. Directory

默认扫描

```
┌──(sec@debian)-[~]
└─$ dirsearch -l ~/httpx_url.txt --format=plain -o ~/dirsearch_default.txt
```

H2-9000低危版本.txt

```
┌──(sec@debian)-[~]
└─$ dirsearch -w ~/H2-9000低危版本.txt -l ~/httpx_url.txt --format=plain -o ~/dirsearch_H2-9000低危版本.txt
```

raft-large-files.txt

```
┌──(sec@debian)-[~]
└─$ dirsearch -w ~/raft-large-files.txt -l ~/httpx_url.txt --format=plain -o ~/dirsearch_raft-large-files.txt
```

raft-large-directories.txt

```
┌──(sec@debian)-[~]
└─$ dirsearch -w ~/raft-large-directories.txt -l ~/httpx_url.txt --format=plain -o ~/dirsearch_raft-large-directories.txt
```

raft-large-words.txt

> 给没有 `.` 的行添加 `.%EXT%` : `sed '/\./! s/$/.%EXT%/' ~/raft-large-words.txt > ~/raft-large-words_EXT.txt` 

```
┌──(sec@debian)-[~]
└─$ dirsearch -w ~/raft-large-words_EXT.txt -e php,phtml,asp,aspx,jsp,jspx,html,shtml,js,cgi -l ~/httpx_url.txt --format=plain -o ~/dirsearch_raft-large-words_EXT.txt
```

生成 `dirsearch_url.txt` , 删除无效 URL 并去重

```
┌──(sec@debian)-[~]
└─$ python3 ./dirsearch_url.py
```

手工访问 `dirsearch_url.txt` 并整理

```
无访问内容的归类为 false.txt
将有访问内容的 URL 归类为 true.txt

并剔除 dirsearch 生成的信息, 仅保留 URL
awk '{print $3}' true.txt > true_url.txt

true_url.txt 中添加跟站点: https://10086.cn:443/
```

### 2.6. Spider

```
┌──(sec@debian)-[~]
└─$ katana -list true_url.txt -iqp -e cdn,private-ips -ef css -o katana_url.txt
```

### 2.7. FingerPrints

whatweb

```
┌──(sec@debian)-[~]
└─$ whatweb -a 3 -v --color=never -i httpx_url.txt | tee whatweb_url.txt
```

wafw00f

```
┌──(sec@debian)-[~]
└─$ wafw00f -a -v -i httpx_url.txt -o wafw00f_url.txt
```

## 3. Scan

```
┌──(sec@debian)-[~]
└─$ nikto -h httpx_url.txt -Format htm -o nikto_url.htm
```

## 4. 筛选

手工访问 `dirsearch_url.txt` , `katana_url.txt` 和 `nikto_ip.htm` 中的 URL, 并将脆弱站点整合到 `url.txt` 

## 5. PoC

```
┌──(sec@debian)-[~]
└─$ nuclei -l url.txt -o nuclei_url.txt
```

## 6. 信息泄露

### 6.1. 扫描仓库

Scan a repo for only verified secrets

```
┌──(sec@debian)-[~]
└─$ trufflehog git https://github.com/10086.cn/test_keys --results=verified,unknown
```

### 6.2. AccessKey 泄露

## 7. 手工测试

访问 `url.txt` 中的每个站点

## 8. 关系梳理

对每个站点进行爬虫

```
┌──(sec@debian)-[~]
└─$ katana -u https://10086.cn:443/test/ -iqp -e cdn,private-ips -ef css -o katana_10086.cn-443-test.txt
```

保存 FindSomething 中的结果

```
findsomething_10086.cn-443-test.txt
```

手工访问每个业务板块, 使用 Xmind 绘制思维导图;

手工测试每个功能点, 使用 Visio 绘制流程图.
