Python is a programming language that lets you work quicklyand integrate systems more effectively.

## 1. Install

```
┌──(sec@debian)-[~]
└─$ sudo apt install -y python3 python3-pip python3-venv python3-dev
```

## 2. Init

配置镜像加速

```
┌──(sec@debian)-[~]
└─$ python3 -m pip config set global.index-url "https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple"
```

## 3. Usage

### 3.1. venv

创建虚拟环境

```
┌──(sec@debian)-[~]
└─$ python3 -m venv ./venv
```

激活虚拟环境

```
┌──(sec@debian)-[~]
└─$ source ./venv/bin/activate
```

退出虚拟环境

```
┌──(sec@debian)-[~]
└─$ deactivate
```

---

References

- [python](https://www.python.org/)
