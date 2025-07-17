字典生成。

## 1 安装

克隆

```shell
┌──(root㉿kali)-[~]
└─# git clone https://github.com/LandGrey/pydictor.git /root/tools/pydictor
```

编写脚本

```shell
┌──(root㉿kali)-[~]
└─# vim /root/tools/pydictor/pydictor.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 pydictor
python3 pydictor.py "$@"
```

创建链接

```shell
┌──(root㉿kali)-[~]
└─# chmod +x /root/tools/pydictor/pydictor.sh && ln -s /root/tools/pydictor/pydictor.sh /usr/local/bin/pydictor
```

## 2 使用

生成全部由数字组成且长度为 4 到 6 位的字典 

```shell
┌──(root㉿kali)-[~]
└─# pydictor -base d --len 4 6
```

生成使用数字、小写字母与大写字母 3 者组合且长度为 6 位的字典，并把生成的字典导出到 /root/passwd.txt

```shell
┌──(root㉿a-kali-23)-[~]
└─# pydictor -base dLc --len 6 6 -o /root/passwd.txt
```

生成含有特殊字符的自定义字符集字典

```shell
┌──(root㉿a-kali-23)-[~]
└─# pydictor -char '@#$%^&*abcdefg12345678' --len 6 6
```

生成以 Pa5sw0rd 开头，后面 4 位全为数字的字典

```shell
┌──(root㉿a-kali-23)-[~]
└─# pydictor -base d --len 4 4 --head Pa5sw0rd
```

将一个目录下多个字典合并去掉重复的记录

```shell
┌──(root㉿a-kali-23)-[~]
└─# pydictor -tool uniqbiner /root/password/
```

**字典合并去重**

查看两个密码文件

```shell
┌──(root㉿a-kali-23)-[~]
└─# cat hello.txt <(echo '---------') world.txt
```

```
hello
666
---------
world
666
```

> echo 使两个文件内容之间生成分隔符，便于区分

## 3 帮助

查看帮助

```shell
┌──(root㉿kali)-[~]
└─# pydictor -h
```

---

References

- [pydictor](https://github.com/LandGrey/pydictor)
