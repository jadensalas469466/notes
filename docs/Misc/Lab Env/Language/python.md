Python is a programming language that lets you work quicklyand integrate systems more effectively.

## 1. Install

### 1.1. Debian

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y python3 python3-pip python3-venv python3-dev
```

### 1.2. Windows

以管理员身份安装并添加到环境变量

![以管理员身份安装并添加到环境变量](./../../../../images/Python/%E4%BB%A5%E7%AE%A1%E7%90%86%E5%91%98%E8%BA%AB%E4%BB%BD%E5%AE%89%E8%A3%85%E5%B9%B6%E6%B7%BB%E5%8A%A0%E5%88%B0%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F.png)

## 2. Init

配置镜像加速

```
┌──(nemo@debian)-[~]
└─$ python3 -m pip config set global.index-url "https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple"
```

```
PS C:\Users\nemo> pip config set global.index-url "https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple"
```

## 3. Usage

### 3.1. venv

创建虚拟环境

```
┌──(nemo@debian)-[~]
└─$ python3 -m venv ./venv
```

```
PS C:\Users\nemo> python -m venv .\venv
```

激活虚拟环境

```
┌──(nemo@debian)-[~]
└─$ source ./venv/bin/activate
```

```
PS C:\Users\nemo> .\venv\Scripts\Activate.ps1
```

> PowerShell 首次运行这行命令需先配置执行策略
>
> ```
> PS C:\Users\nemo> Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
> 
> Execution Policy Change
> The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
> you to the security risks described in the about_Execution_Policies help topic at
> https:/go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
> [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): A
> ```

退出虚拟环境

```
┌──(venv)─(nemo@debian)-[~]
└─$ deactivate
```

```
(venv) PS C:\Users\nemo> deactivate
```

---

References

- [Python](https://www.python.org/)

