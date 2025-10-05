Python is a programming language that lets you work quicklyand integrate systems more effectively.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y python3 python3-pip python3-venv python3-dev
```

## 2. Init

配置镜像加速

```
┌──(nemo@debian)-[~]
└─$ python3 -m pip config set global.index-url "https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple"
```

## 3. Usage

### 3.1. venv

创建虚拟环境

```
┌──(nemo@debian)-[~/path]
└─$ python3 -m venv ./venv
```

```
PS C:\Users\nemo\path> python -m venv .\venv
```

激活虚拟环境

```
┌──(nemo@debian)-[~/path]
└─$ source ./venv/bin/activate
```

```
PS C:\Users\nemo\path\> .\venv\Scripts\Activate.ps1
```

退出虚拟环境

```
┌──(venv)─(nemo@debian)-[~/path]
└─$ deactivate
```

```
(venv) PS C:\Users\nemo\path> deactivate
```

---

References

- [Python](https://www.python.org/)

