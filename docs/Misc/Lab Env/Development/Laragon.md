Modern & Powerful - Easy Operation
Productive. Portable. Fast. Effective. Awesome!

## 1. Install

取消推荐配置

![取消推荐配置](./../../../../image/Laragon/%E5%8F%96%E6%B6%88%E6%8E%A8%E8%8D%90%E9%85%8D%E7%BD%AE.png)

## 2. Init

修改协议配置

```
C:\laragon\etc\apache2\httpd-ssl.conf
```

```
7 SSLProtocol TLSv1.2 TLSv1.3
8 SSLProxyProtocol TLSv1.2 TLSv1.3
SSLProtocol all -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
SSLProxyProtocol all -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
```

## 3. Usage

### 3.1. 更换程序版本

将下载的程序解压到以下对应的目录

```
C:\laragon\bin\apache
C:\laragon\bin\mysql
C:\laragon\bin\php
```

在主界面右键切换到对应的版本

![在主界面右键切换到对应的版本](./../../../../image/Laragon/%E5%9C%A8%E4%B8%BB%E7%95%8C%E9%9D%A2%E5%8F%B3%E9%94%AE%E5%88%87%E6%8D%A2%E5%88%B0%E5%AF%B9%E5%BA%94%E7%9A%84%E7%89%88%E6%9C%AC.png)

### 3.2. 为数据库配置密码

运行数据库后打开终端

![运行数据库后打开终端](./../../../../image/Laragon/%E8%BF%90%E8%A1%8C%E6%95%B0%E6%8D%AE%E5%BA%93%E5%90%8E%E6%89%93%E5%BC%80%E7%BB%88%E7%AB%AF.png)

修改密码

```
mysql -u root -p
```

```
Enter password:
```

```
MariaDB [(none)]> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('123456');
MariaDB [(none)]> exit;
```

---

- [Laragon](https://laragon.org/)

