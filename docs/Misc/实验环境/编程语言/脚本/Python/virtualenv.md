一个用于创建独立 Python 虚拟环境的工具。

## 1 部署

debian 中安装

```shell
root@debian:~# apt install -y virtualenv
```

Windows 中安装

```powershell
PS C:\Users\sec> pip install virtualenv
```

## 2 使用

创建虚拟环境

```shell
root@debian:~# virtualenv venv
```

启用虚拟环境

```shell
root@debian:~# source venv/bin/activate
```

Powershell 需要允许脚本执行

```powershell
PS C:\Users\sec> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
```

再启用虚拟环境

```powershell
PS C:\Users\sec> .\venv\Scripts\Activate
```

在虚拟环境中安装依赖

```shell
(venv) root@debian:~# pip3 install -r requirements.txt
```

退出虚拟环境

```shell
(venv) root@debian:~# deactivate
```

---

参考链接

- [virtualenv](https://github.com/pypa/virtualenv/)
- [virtualenv Documentation](https://virtualenv.pypa.io/en/latest/)
