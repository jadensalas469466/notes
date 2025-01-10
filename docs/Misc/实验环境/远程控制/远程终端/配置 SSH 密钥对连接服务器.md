1. 在客户端生成一对密钥（公钥和私钥）
2. 将公钥复制到服务器的 `~/.ssh/authorized_keys` 文件中
3. 当客户端尝试连接服务器时，服务器使用公钥验证客户端私钥的签名，确保只有持有正确私钥的用户可以访问

## 1 生成密钥对

生成一对 步骤H 密钥

```powershell
PS C:\Users\sec> ssh-keygen -t ed25519 -f C:\Users\sec\.ssh\ssh-test
```

```
Generating public/private ed25519 key pair.
Enter passphrase (empty for no passphrase):123456
Enter same passphrase again:123456
Your identification has been saved in C:\Users\sec\.ssh\ssh-test
Your public key has been saved in C:\Users\sec\.ssh\ssh-test.pub
The key fingerprint is:
SHA256:cr8ZyfprzEIKUvvBLrxmDObdwDbglIJiTlw/b2TvbPc sec@desktop
The key's randomart image is:
+--[ED25519 256]--+
|                 |
|   .             |
|o ...            |
|+++ .o o         |
|=+ + o* S        |
| .= B o=.+ .     |
| o B B.+oo=      |
|  . B = .=+=     |
|   o.o  o+*..E   |
+----[SHA256]-----+
```

查看 SSH 密钥对

```powershell
PS C:\Users\sec> ls C:\Users\sec\.ssh\
```

```
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        2024/10/24     21:44            444 ssh-test
-a----        2024/10/24     21:44             94 ssh-test.pub
```

## 2 保存私钥到 ssh-agent

运行 ssh-agent 服务

```powershell
PS C:\Users\sec> Start-Service ssh-agent
```

配置 ssh-agent 服务开机自启

```powershell
PS C:\Users\sec> Get-Service ssh-agent | Set-Service -StartupType Automatic
```

查看 ssh-agent 服务状态

```powershell
PS C:\Users\sec> Get-Service ssh-agent
```

```
Status   Name               DisplayName
------   ----               -----------
Running  ssh-agent          OpenSSH Authentication Agent
```

保存 SSH 私钥到 ssh-agent

```powershell
PS C:\Users\sec> ssh-add $env:USERPROFILE\.ssh\ssh-test
```

```
Enter passphrase for C:\Users\sec\.ssh\ssh-test:123456
Identity added: C:\Users\sec\.ssh\ssh-test (sec@desktop)
```

列出 ssh-agent 中保存的私钥

```powershell
PS C:\Users\sec> ssh-add -l
```

> 从 ssh-agent 中移除指定私钥
>
> ```powershell
> PS C:\Users\sec> ssh-add -d $env:USERPROFILE\.ssh\ssh-test
> ```
>
> 从 ssh-agent 中移除所有私钥
>
> ```powershell
> PS C:\Users\sec> ssh-add -D
> ```

## 3 部署公钥到服务器

复制公钥内容到剪切板

```powershell
PS C:\Users\sec> Get-Content $env:USERPROFILE\.ssh\ssh-test.pub | Set-Clipboard
```

将复制的内容写入 `~/.ssh/authorized_keys` 文件

```shell
root@server:~# vim ~/.ssh/authorized_keys
```

> 若为 Windows 服务器则可以使用如下方法：
>
> 1. 读取公钥内容到 $authorizedKey 变量
>
>    ```powershell
>    PS C:\Users\sec> $authorizedKey = Get-Content -Path $env:USERPROFILE\.ssh\ssh-test.pub
>    ```
>
> 2. 设置 $remotePowerShell 变量将 $authorizedKey 变量写入到服务器上的 authorized_keys 文件
>
>    ```powershell
>    PS C:\Users\sec> $remotePowershell = "powershell New-Item -Force -ItemType Directory -Path $env:USERPROFILE\.ssh; Add-Content -Force -Path $env:USERPROFILE\.ssh\authorized_keys -Value '$authorizedKey'"
>    ```
>
> 3. 连接 Windows 服务器并运行 $remotePowerShell 变量
>
>    ```powershell
>    PS C:\Users\sec> ssh sec@windows.local $remotePowershell
>    ```

## 4 配置使用密钥对登录

启用密钥对登录并禁止密码登录

```shell
root@server:~# vim /etc/ssh/sshd_config
```

```
38 PubkeyAuthentication yes
57 PasswordAuthentication no
```

重启 SSH 服务

```shell
root@server:~# systemctl restart sshd.service
```

> Windows 重启 SSH 服务：
>
> ```powershell
> PS C:\Users\sec> Restart-Service sshd
> ```

完成后可将密钥对备份到一个安全位置，然后将其从本地系统中删除，若要配置 SFTP 记得保留私钥

---

参考链接

- [适用于 Windows 的 OpenSSH 入门](https://learn.microsoft.com/zh-cn/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui&pivots=windows-server-2025)
- [OpenSSH for Windows 中基于密钥的身份验证](https://learn.microsoft.com/zh-cn/windows-server/administration/openssh/openssh_keymanagement)