分布式版本控制系统.

```
工作区 add-> 暂存区 commit-> 本地仓库 <-pull||push-> 远程仓库
```

> HEAD 指的是最新一次的提交

## 1. 安装

Windows 安装

```
PS C:\Users\sec> scoop install git
```

Linux 安装

```
┌──(root@debian)-[~]
└─# apt install -y git
```

## 2. 初始化

在 Github 开启私人电子邮箱

![在 Github 开启私人电子邮箱](./../../../../images/Git/%E5%9C%A8%20Github%20%E5%BC%80%E5%90%AF%E7%A7%81%E4%BA%BA%E7%94%B5%E5%AD%90%E9%82%AE%E7%AE%B1.png)

选择平局管理器

![选择平局管理器](./../../../../images/Git/%E9%80%89%E6%8B%A9%E5%B9%B3%E5%B1%80%E7%AE%A1%E7%90%86%E5%99%A8.png)

### 2.1. Windows

配置代理

```
PS C:\Users\sec> git config --global http.proxy "http://127.0.0.1:10809"
```

配置使用 Windows 证书校验

```
PS C:\Users\sec> git config --global http.sslBackend schannel
```

配置用户名

```
PS C:\Users\sec> git config --global user.name "sec"
```

配置邮箱

```
PS C:\Users\sec> git config --global user.email "<private-name>@users.noreply.github.com"
```

禁止自动转换换行符

```
PS C:\Users\sec> git config --global core.autocrlf false
```

配置对文件名大小写敏感

```
PS C:\Users\sec> git config --global --get core.ignorecase
```

### 2.2. Linux

配置代理

```
┌──(root@debian)-[~]
└─# git config --global http.proxy 'http://192.168.1.201:10809'
```

限制 HTTP 协议版本

```
┌──(root@debian)-[~]
└─# git config --global http.version HTTP/1.1
```

## 3. 使用

### 3.1. 基础

克隆仓库

```
git clone <repository-url>           # 完整克隆
git clone --depth 1 <repository-url> # 只克隆最新的一次提交
```

添加到暂存区

```
git add .      # 全部文件
git add <file> # 指定文件
```

提交到本地仓库

```
git commit -m "comment"
```

与远程仓库同步

```
git push # 从本地推送到远程
git pull # 从远程拉取到本地
```

### 3.2. 进阶

查看提交日志

```
git log           # Commit ID + Author + Date + Comment
git log --stat    # Commit ID + Author + Date + Comment + Changes
git log --oneline # Commit ID + Comment
```

查看提交内容

```
git show HEAD        # 查看最新提交的内容
git show <commit-id> # 查看指定提交的内容
git show <branch>    # 查看指定分支最新提交的内容
```

查看更改或比较

```
git diff          # 查看工作区已更改但未添加到暂存区的文件
git diff HEAD     # 查看工作区已更改但未提交到本地仓库的文件
git diff --staged # 查看已添加到暂存区但未提交到本地仓库的文件
git diff <commit-id-1> <commit-id-2> # 比较两个提交之间的差异
git diff <branch-1> <branch-2>       # 比较两个分支之间的差异
```

撤回

```
git revert <commit-id>      # 撤回某次提交并提交最新状态到本地仓库
git revert -m 1 <commit-id> # 撤回指定分支的某次提交并提交最新状态到本地仓库
```

回退

```
git reset HEAD^       # 回退到最新提交前的第一个版本
git reset HEAD~1      # 回退到最新提交前的第一个版本
git reset HEAD~3      # 回退到最新提交前的第三个版本
git reset HEAD~1 File # 指定文件回退到最新提交前的第一个版本
git reset --soft <commit-id>  # 回退到已添加到暂存区但未提交到本地仓库时
git reset --mixed <commit-id> # 回退到工作区已改动但未添加到暂存区时 (默认)
git reset --hard <commit-id>  # 回退到工作区未改动时
```

切换提交节点但不重置

```
git checkout <commit-id>
```

### 3.3. 发布

### 3.3.1. 快速发布

在 GitHub 创建一个仓库, 克隆仓库到本地即可

```
git clone <repository-url>
```

### 3.3.2. 标准发布

在 GitHub 创建一个空仓库

进入本地项目目录

```shell
root@debian:~# cd ./test
```

初始化仓库

```shell
root@debian:~# git init
```

命名默认分支为 `main` 

```shell
root@debian:~# git branch -M main
```

配置远程仓库

```shell
root@debian:~# git remote add origin https://github.com/<user-name>/test.git
```

创建 `README.md` 文件

```shell
root@debian:~# echo "test" > README.md
```

暂存指定文件的更改

```shell
root@debian:~# git add README.md
```

提交

```shell
root@debian:~# git commit -m "first commit"
```

推送到远程仓库的指定分支 `main` 

```shell
root@debian:~# git push -u origin main
```

### 3.4. 配置

### 3.4.1. 全局配置

列出全局配置

```shell
┌──(root㉿kali-23)-[~]
└─# git config --global --list
```

查看源

```shell
┌──(root㉿kali)-[~]
└─# git config --global --get-regexp "url\..*\.insteadOf"
```

配置源

```shell
┌──(root㉿kali)-[~]
└─# git config --global url."https://ghp.ci/https://github.com/".insteadOf https://github.com/
```

移除源

```shell
┌──(root㉿kali)-[~]
└─# git config --global --unset url."https://ghp.ci/https://github.com/.insteadOf"
```

查看代理

```shell
┌──(root㉿kali)-[~]
└─# git config --global http.proxy
```

配置代理

```shell
┌──(root㉿kali)-[~]
└─# git config --global http.proxy "http://127.0.0.1:10809"
```

移除代理

```shell
┌──(root㉿kali)-[~]
└─# git config --global --unset http.proxy
```

### 3.4.1. 部署 SSH 到 GitHub

使用 OpenSSH 部署公钥到 Git 服务器

![使用 OpenSSH 部署公钥到 Git 服务器](./../../../../images/Git/%E4%BD%BF%E7%94%A8%20OpenSSH%20%E9%83%A8%E7%BD%B2%E5%85%AC%E9%92%A5%E5%88%B0%20Git%20%E6%9C%8D%E5%8A%A1%E5%99%A8.png)

配置 Git 使用 Windows SSH 客户端

```powershell
PS C:\Users\sec> git config --global core.sshCommand "C:/Windows/System32/OpenSSH/ssh.exe"
```

## 4. 帮助

```shell
sec@a MINGW64 ~
$ git -h
```

```
用法：git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           [--config-env=<name>=<envvar>] <command> [<args>]

这些是在各种情况下使用的常见 Git 命令：

开始一个工作区（也可参阅：git 帮助 教程）
   clone     将存储库克隆到新目录中
   init      创建一个空的 Git 存储库或重新初始化现有存储库

处理当前更改（也可参阅：git 帮助 日常）
   add       将文件内容添加到索引中
   mv        移动或重命名文件、目录或符号链接
   restore   恢复工作树文件
   rm        从工作树和索引中删除文件

检查历史记录和状态（也可参阅：git 帮助 修订）
   bisect    使用二分搜索找到引入错误的提交
   diff      显示提交之间的更改，提交和工作树之间的更改等
   grep      打印匹配模式的行
   log       显示提交日志
   show      显示各种类型的对象
   status    显示工作树状态

增长、标记和调整您的常见历史记录
   branch    列出、创建或删除分支
   commit    记录对存储库的更改
   merge     将两个或多个开发历史记录合并在一起
   rebase    在另一个基本尖端之上重新应用提交
   reset     将当前 HEAD 重置为指定状态
   switch    切换分支
   tag       创建、列出、删除或验证用 GPG 签名的标签对象

合作（也可参阅：git 帮助 工作流程）
   fetch     从另一个存储库下载对象和引用
   pull      从另一个存储库或本地分支获取并集成
   push      更新远程引用以及关联的对象

'git help -a' 和 'git help -g' 列出可用的子命令和一些概念指南。
请参阅 'git help <command>' 或 'git help <concept>' 了解特定子命令或概念。
请参阅 'git help git' 以获取系统概述。
```

---

参考链接

- [Git](https://github.com/git/git)
