基于SpringBoot、Shiro、Mybatis的权限后台管理系统

## 1. Fingerprint

### 1.1. Logo

![logo](./../../../../images/RuoYi/logo.png)

### 1.2. Favicon

HUNTER

```
web.icon="e49fd30ea870c7a820464ca56a113e6e"||web.icon="4eeb8a8eb30b70af511dcc28c11a3216"
```

FOFA

```
icon_hash="-1231872293" || icon_hash="706913071"
```

QUAKE

```
favicon:"e49fd30ea870c7a820464ca56a113e6e" OR favicon:"4eeb8a8eb30b70af511dcc28c11a3216"
```

ZoomEye

```
iconhash="e49fd30ea870c7a820464ca56a113e6e" || iconhash="4eeb8a8eb30b70af511dcc28c11a3216"
```

### 1.3. Frontend Page

![Frontend Page](./../../../../images/RuoYi/Frontend%20Page.png)

### 1.4. Backend Page

![Backend Page](./../../../../images/RuoYi/Backend%20Page.png)

### 1.5. Loading Page

![Loading Page](./../../../../images/RuoYi/Loading%20Page.gif)

## 2. 环境搭建

安装依赖

```
 RuoYi = 4.8.1
  JDK >= 1.8
Maven >= 3.0
MySQL >= 5.7
```

```
RuoYi = 4.2.0
 JDK >= 17
```

克隆仓库

```
┌──(nemo@debian)-[~]
└─$ git clone https://github.com/yangzongzhuan/RuoYi.git
```

创建数据库

```
┌──(nemo@debian)-[~]
└─$ mysql -u root -p
```

```
MariaDB [(none)]> CREATE DATABASE ry
CHARACTER SET utf8
COLLATE utf8_general_ci;
USE ry;
```

导入数据库文件

```
MariaDB [ry]> SOURCE /home/nemo/RuoYi/sql/quartz.sql
SOURCE /home/nemo/RuoYi/sql/ry_20191008.sql
EXIT;
```

修改配置文件

```
┌──(nemo@debian)-[~]
└─$ sed -i.bak '0,/password: password/{s/password: password/password: 123456/}' ~/RuoYi/ruoyi-admin/src/main/resources/application-druid.yml \
&& sed -i.bak '0,/port: 80/{s/port: 80/port: 60081/}' ~/RuoYi/ruoyi-admin/src/main/resources/application.yml
```

创建日志目录

```
┌──(nemo@debian)-[~]
└─$ sudo mkdir -p /home/ruoyi/logs \
&& sudo chmod 755 /home/ruoyi/logs \
&& sudo chown $USER:$USER /home/ruoyi/logs
```

打包

```
┌──(nemo@debian)-[~]
└─$ mvn -f ~/RuoYi/pom.xml clean package
```

运行

```
┌──(nemo@debian)-[~]
└─$ nohup java -jar ~/RuoYi/ruoyi-admin/target/ruoyi-admin.jar > ~/nohup.log 2>&1 & echo $! > ~/pid.log
```

Port Forwarding Rules

| Name  | Host Port | Guest Port |
| ----- | --------- | ---------- |
| RuoYi | 60081     | 60081      |

Visit

> http://127.0.0.1:60081

Login

```
admin:admin123
```

## 3. Nday

### 3.1. Frontend

明文密码泄露

![明文密码泄露](./../../../../images/RuoYi/%E6%98%8E%E6%96%87%E5%AF%86%E7%A0%81%E6%B3%84%E9%9C%B2.png)

弱口令

```
username：admin ruoyi druid            
password：123456 admin druid admin123 admin888
```

[CVE-2019-12422](https://hackerone.com/hacktivity/cve_discovery?id=CVE-2019-12422) (RuoYi < 4.2.0, ==已修复: AES-CBC -> AES-GCM==)

[CVE-2016-4437](https://hackerone.com/hacktivity/cve_discovery?id=CVE-2016-4437)   (RuoYi ≤ 4.6.2, ==已修复: 默认配置随机密钥==)

```
RuoYi ≤ 4.3.0
```

```
fCq+/xW488hMTCD+cmJ3aQ==
```

```
4.3.0 < RuoYi ≤ 4.6.2
```

```
zSyK5Kp6PZAAjlT+eeNMlg==
```

---

References

- [RuoYi](https://github.com/yangzongzhuan/RuoYi)
- [历史漏洞](https://doc.ruoyi.vip/ruoyi/document/kslj.html#%E5%8E%86%E5%8F%B2%E6%BC%8F%E6%B4%9E)
- [若依(RuoYi)框架漏洞战争手册](https://mp.weixin.qq.com/s/JXH3rfDzlIgz0euyPYSLlg)
- [若依Vue前后端分离渗透测试的一些技巧](https://mp.weixin.qq.com/s/IZQacNfVOdoGd-ylzfyQlA)

