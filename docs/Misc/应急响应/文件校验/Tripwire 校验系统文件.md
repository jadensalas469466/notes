# 

用于对系统文件进行校验。

## 1 安装

安装 Tripwire

```
[root@CentOS-76 ~]# yum install -y tripwire
```

## 2 配置

创建六个密码

```
[root@CentOS-76 ~]# tripwire-setup-keyfiles
```

> 都设置为 `123456` 即可

查看配置文件

```
[root@CentOS-76 ~]#  ls /etc/tripwire/
CentOS-76-local.key  site.key  tw.cfg  twcfg.txt  tw.pol  twpol.txt
```

| 文件        | 描述        |
| --------- | --------- |
| site.key  | 用于保护策略文件  |
| local.key | 用于保护数据库文件 |
| tw.pol    | 策略文件      |
| twpol.txt | 策略文件的易读格式 |

## 3 初始化

生成系统校验数据并写入数据库

```
[root@CentOS-76 ~]# tripwire --init
```

```
Please enter your local passphrase: 
Parsing policy file: /etc/tripwire/tw.pol
Generating the database...
*** Processing Unix File System ***
### Warning: File system error.
### Filename: /usr/sbin/fixrmtab
### 没有那个文件或目录
### Continuing...
### Warning: File system error.
### Filename: /usr/share/grub/i386-redhat/e2fs_stage1_5
### 没有那个文件或目录
### Continuing...
Wrote database file: /var/lib/tripwire/CentOS-76.twd
The database was successfully generated.
```

> 校验的结果写入到了 `/var/lib/tripwire/CentOS-76.twd` 数据库文件中

> 可以看到有很多不存在的目录 `没有那个文件或目录`
> 
> 这是由于 tripwire 是一个通用的校验系统的软件，并没有针对某个系统校验
> 
> 可以修改策略文件，定制自己的校验策略

打开 `/etc/tripwire/twpol.txt` ，注释掉不需要校验的文件路径，有需要校验的取消注释即可

```
[root@CentOS-76 ~]# vim /etc/tripwire/twpol.txt
```

> 生成校验数据以后，可以使用 `tripwire --check` 对系统进行校验

校验系统，提取出不存在的路径

```
[root@CentOS-76 ~]# tripwire --check | grep Filename > no-directory.txt
```

写一个脚本

```
[root@CentOS-76 ~]# vim twpol.sh
```

```bash
for f in $(grep "Filename:" no-directory.txt | cut -f2 -d:); do
sed -i "s|\($f\) |#\\1|g" /etc/tripwire/twpol.txt
done
```

> 将 `no-directory.txt` 与  `/etc/tripwire/twpol.txt` 中的路径进行对比，注释这些路径

执行脚本

```
[root@CentOS-76 ~]# bash twpol.sh
```

启用策略文件

```
[root@CentOS-76 ~]# twadmin -m P /etc/tripwire/twpol.txt 
```

重新生成系统校验数据并写入数据库

```
[root@CentOS-76 ~]# tripwire --init
```

> 此次生成的校验数据没有报错

## 4 使用 tripwire 校验系统文件

更改系统文件

```
[root@CentOS-76 ~]# echo aaa >> /etc/passwd
```

添加一个用户

```
[root@CentOS-76 ~]# useradd abc
```

### 4.1 对系统进行完整检查

```
[root@CentOS-76 ~]# tripwire --check
```

```
Modified:
"/etc/group"

-------------------------------------------------------------------------------
Rule Name: Critical configuration files (/etc/group-)
Severity Level: 100
-------------------------------------------------------------------------------

Modified:
"/etc/group-"

-------------------------------------------------------------------------------
Rule Name: Critical configuration files (/etc/passwd)
Severity Level: 100
-------------------------------------------------------------------------------

Modified:
"/etc/passwd"

===============================================================================
Error Report: 
===============================================================================

No Errors

-----------------------------------------------------------------------------*** End of report ***
```

可以看到这些位置发生了改动

### 4.2 指定文件或目录进行校验

```
[root@CentOS-76 ~]# tripwire --check /etc/passwd 
```

```
[root@CentOS-76 ~]# tripwire --check /etc/
```

当系统有变化时记得更新数据库

```
[root@CentOS-76 ~]# tripwire --init
```

### 4.3 添加自定义规则

在配置文件后追加规则用于校验 sqli-labs  的完整性

```
[root@CentOS-76 ~]# vim /etc/tripwire/twpol.txt
```

```
# Ruleset for Sqli-labs
 (
rulename = " Sqli-labs Data",
severity= $(SIG_HI)
 )
 {
 /var/www/html/sqli-labs -> $(SEC_CRIT);
 }
```

> 规则名为 `Sqli-labs D`
> 
> 严重程度为 `SIG_HI`
> 
> 路径为 `/var/www/html/sql`

启用策略

```
[root@CentOS-76 ~]# twadmin -m P /etc/tripwire/twpol.txt
```

更新校验数据库

```
[root@CentOS-76 ~]# tripwire --init
```

检查 sqli-labs 目录

```
[root@CentOS-76 ~]# tripwire --check /var/www/html/sqli-labs
```

---

参考连接

- [Tripwire](https://www.tripwire.com/)
