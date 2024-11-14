使用 Git 时出现的一些错误及其解决方法。

# 1 Git 部署 SSH 公钥后无法使用 SSH 操作

在网络环境不佳时，我们往往会配置 SSH 用于连接 Git 服务器

将公钥部署到 Git 服务器后，使用 SSH 进行 Git 操作会出现以下错误

![将公钥部署到 Git 服务器后，使用 SSH 进行 Git 操作可能会出现以下错误](./../../../images/Git%20%E7%9A%84%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98/%E5%B0%86%E5%85%AC%E9%92%A5%E9%83%A8%E7%BD%B2%E5%88%B0%20Git%20%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%90%8E%EF%BC%8C%E4%BD%BF%E7%94%A8%20SSH%20%E8%BF%9B%E8%A1%8C%20Git%20%E6%93%8D%E4%BD%9C%E5%8F%AF%E8%83%BD%E4%BC%9A%E5%87%BA%E7%8E%B0%E4%BB%A5%E4%B8%8B%E9%94%99%E8%AF%AF.png)

这是由于配置时使用的是 Powershell 的 SSH 服务，而 Git 时使用的是自带的 SSH 服务

使用以下命令将 Git 的 SSH 服务修改为 Powershell 的 SSH 服务即可

```powershell
PS C:\Users\sec> git config --global core.sshCommand "C:/Windows/System32/OpenSSH/ssh.exe"
```

![使用以下命令将 Git 的 SSH 服务修改为 Powershell 的 SSH 服务即可](./../../../images/Git%20%E7%9A%84%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98/%E4%BD%BF%E7%94%A8%E4%BB%A5%E4%B8%8B%E5%91%BD%E4%BB%A4%E5%B0%86%20Git%20%E7%9A%84%20SSH%20%E6%9C%8D%E5%8A%A1%E4%BF%AE%E6%94%B9%E4%B8%BA%20Powershell%20%E7%9A%84%20SSH%20%E6%9C%8D%E5%8A%A1%E5%8D%B3%E5%8F%AF.png)

# 2 Git 操作时显示主机密钥验证失败

```
> git pull --tags origin master
CreateProcessW failed error:193
ssh_askpass: posix_spawnp: Unknown error
Host key verification failed.
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

可能是删除缓存造成的

```powershell
PS C:\Windows\system32> Remove-Item C:\Users\sec\.ssh\known_hosts
```

在客户端重新加载 Github 的缓存即可

```powershell
PS C:\Users\sec> ssh -T git@github.com
The authenticity of host 'github.com (20.205.243.166)' can't be established.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

---

参考链接

- [Git](https://git-scm.com/)
- [Git Documentation](https://git-scm.com/doc)
