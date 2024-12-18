用于手动创建独立 Python 虚拟环境的工具, 推荐在复杂的开发环境下使用.

## Debian

## 1 部署

安装

```shell
root@debian:~# apt install -y virtualenv
```

## 2 使用

创建虚拟环境

```shell
root@debian:~# virtualenv /path/venv
```

启用虚拟环境

```shell
root@debian:~# source /path/venv/bin/activate
```

在虚拟环境中安装依赖

```shell
(venv) root@debian:~# pip3 install -r /path/requirements.txt
```

退出虚拟环境

```shell
(venv) root@debian:~# deactivate
```

## Windows

## 1 部署

安装

```powershell
PS C:\Users\sec> pip install virtualenv
```

## 2 使用

创建虚拟环境

```powershell
PS C:\Users\sec> virtualenv \path\venv
```

Powershell 允许脚本执行

```powershell
PS C:\Users\sec> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
```

启用虚拟环境

```powershell
PS C:\Users\sec> \path\venv\Scripts\Activate.ps1
```

在虚拟环境中安装依赖

```powershell
(venv) PS C:\Users\sec> pip3 install -r \path\requirements.txt
```

退出虚拟环境

```powershell
(venv) PS C:\Users\sec> deactivate
```

---

参考链接

- [virtualenv](https://virtualenv.pypa.io/en/latest/)
