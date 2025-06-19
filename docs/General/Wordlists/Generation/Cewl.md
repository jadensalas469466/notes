字典生成。

## 1 使用

扫描目标时深度为 2 ，最小单词长度为 5 ，保存到文件 /root/docswords.txt

```shell
root@kali:~# cewl -d 2 -m 5 -w /root/docswords.txt http://a-centos7-6.local/pikachu/
```

查看帮助

```shell
┌──(root㉿a-kali-23)-[~]
└─# cewl -h
```

```
CeWL 6.1 (Max Length) Robin Wood (robin@digi.ninja) (https://digi.ninja/)
Usage: cewl [OPTIONS] ... <url>

    OPTIONS:
        -h, --help: 显示帮助。
        -k, --keep: 保留下载的文件。
        -d <x>,--depth <x>: 爬虫深度，默认为 2。
        -m, --min_word_length: 最小单词长度，默认为 3。
        -x, --max_word_length: 最大单词长度，默认未设置。
        -o, --offsite: 允许爬虫访问其他网站。
        --exclude: 一个包含要排除的路径列表的文件
        --allowed: 路径必须匹配的正则表达式模式，以便进行跟随
        -w, --write: 将输出结果写入文件。
        -u, --ua <agent>: 要发送的用户代理。
        -n, --no-words: 不输出单词表。
        -g <x>, --groups <x>: 同时返回单词组
        --lowercase: 小写所有已解析的单词
        --with-numbers: 接受包含数字和字母的单词
        --convert-umlauts: 将常见的 ISO-8859-1 (Latin-1) 字符中的 umlauts 转换没有 umlauts 的形式 (ä-ae, ö-oe, ü-ue, ß-ss)
        -a, --meta: 包括元数据。
        --meta_file file: 元数据的输出文件。
        -e, --email: 包括电子邮件地址。
        --email_file <file>: 电子邮件地址的输出文件。
        --meta-temp-dir <dir>: exiftool 解析文件时使用的临时目录，默认为 /tmp。
        -c, --count: 显示找到的每个单词的计数。
        -v, --verbose: 冗余。
        --debug: 额外的调试信息。

        Authentication
        --auth_type: 摘要或基本信息。
        --auth_user: 验证用户名。
        --auth_pass: 验证密码。

        Proxy Support
        --proxy_host: 代理服务器
        --proxy_port: 代理端口，默认为 8080。
        --proxy_username: 代理用户名（如需要）。
        --proxy_password: 代理密码（如需要）。

        Headers
        --header, -H: 格式为 name:value - 可以传递多个。

    <url>: 网站爬虫。
```

查看手册

```shell
┌──(root㉿a-kali-23)-[~]
└─# man cewl > cewl.txt && cat cewl.txt
```

```
cewl(1)          custom word list generator         cewl(1)

NAME
       cewl - 自定义单词表生成器

SYNOPSIS
       cewl [OPTION] ... URL

DESCRIPTION
       CeWL（自定义单词表生成器）是一款 Ruby 应用程序，它可以在指定深度内对给定的 URL 进行爬虫，并返回单词表，该单词表可用于密码破解，如 John the  Ripper。 
       另外，CeWL 还可以跟踪外部链接。

       CeWL 还可以创建在 mailto 链接中发现的电子邮件地址列表。
       这些电子邮件地址可在暴力破解行动中用作用户名。

       CeWL 的读音是 "cool".

OPTIONS
       常规选项

        -h, --help: 显示帮助。
        -k, --keep: 保留下载的文件。
        -d <x>,--depth <x>: 爬虫深度，默认为 2。
        -m, --min_word_length: 最小单词长度，默认为 3。
        -x, --max_word_length: 最大单词长度，默认未设置。
        -o, --offsite: 允许爬虫访问其他网站。
        --exclude: 一个包含要排除的路径列表的文件
        --allowed: 路径必须匹配的正则表达式模式，以便进行跟随
        -w, --write: 将输出结果写入文件。
        -u, --ua <agent>: 要发送的用户代理。
        -n, --no-words: 不输出单词表。
        -g <x>, --groups <x>: 同时返回单词组
        --lowercase: 小写所有已解析的单词
        --with-numbers: 接受包含数字和字母的单词
        --convert-umlauts: 将常见的 ISO-8859-1 (Latin-1) 字符中的 umlauts 转换没有 umlauts 的形式 (ä-ae, ö-oe, ü-ue, ß-ss)
        -a, --meta: 包括元数据。
        --meta_file file: 元数据的输出文件。
        -e, --email: 包括电子邮件地址。
        --email_file <file>: 电子邮件地址的输出文件。
        --meta-temp-dir <dir>: exiftool 解析文件时使用的临时目录，默认为 /tmp。
        -c, --count: 显示找到的每个单词的计数。
        -v, --verbose: 冗余。
        --debug: 额外的调试信息。

        Authentication
        --auth_type: 摘要或基本信息。
        --auth_user: 验证用户名。
        --auth_pass: 验证密码。

        Proxy Support
        --proxy_host: 代理服务器
        --proxy_port: 代理端口，默认为 8080。
        --proxy_username: 代理用户名（如需要）。
        --proxy_password: 代理密码（如需要）。

        Headers
        --header, -H: 格式为 name:value - 可以传递多个。

        <url>: 网站爬虫。

TIP
       有时，CeWL 什么也不会返回。
       使用 -v 选项可查看导致无输出的问题。 
       例如：如果"$ cewl http://example.org "被重定向到 https://example.org，cewl 将保持静默。

BUGS
       有人报告说，爬虫会漏掉一些有查询字符串的页面。 这一点尚未得到证实。

SEE ALSO
       fab-cewl(1)

AUTHOR
       CeWL 由 Robin Wood 撰写
       <robin@digi.ninja>。

       本手册由 Joao Eriberto Mota
       Filho <eriberto@debian.org> 为 Debian 项目撰写。
       (但也可用于其他项目）。

cewl-6.0                26 Jul 2023                 cewl(1)
```

---

Refrences

- [Cewl](https://www.kali.org/tools/cewl/)
