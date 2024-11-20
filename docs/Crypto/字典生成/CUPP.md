字典生成。

## 1 部署

安装

```shell
┌──(root㉿a-kali-23)-[~]
└─# sudo apt install -y cupp
```

## 2 使用

输入已知信息生成字典

```shell
┌──(root㉿a-kali-23)-[~]
└─# cupp -i
```

```
 ___________ 
   cupp.py!                 # Common
      \                     # User
       \   ,__,             # Passwords
        \  (oo)____         # Profiler
           (__)    )\   
              ||--|| *      [ Muris Kurgas | j0rgan@remote-exploit.org ]
                            [ Mebus | https://github.com/Mebus/]


[+] Insert the information about the victim to make a dictionary
[+] If you don't know all the info, just hit enter when asked! ;)

> First Name: 
```

## 3 帮助

查看帮助

```shell
┌──(root㉿a-kali-23)-[~]
└─# cupp -h
```

```
usage: cupp [-h] [-i | -w FILENAME | -l | -a | -v] [-q]

Common User Passwords Profiler

options:
  -h, --help         显示此帮助信息并退出
  -i, --interactive  用于分析用户密码的互动问题
  -w FILENAME        使用此选项改进现有词典，或使用 WyD.pl 输出制作一些常见密码
  -l                 从资源库下载大量词表
  -a                 直接从 Alecto 数据库解析默认用户名和密码。
                     Alecto 项目使用经过净化的 Phenoelit 和 CIRT 数据库，并对其进行了合并和增强。
  -v, --version      显示该程序的版本。
  -q, --quiet        静默模式（不打印横幅）
```

查看手册

```shell
┌──(root㉿a-kali-23)-[~]
└─# man cupp > cupp.txt && cat cupp.txt
```

---

参考链接

- [CUPP](https://github.com/Mebus/cupp)
