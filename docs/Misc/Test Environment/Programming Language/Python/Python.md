Python is powerful... and fast;
plays well with others;
runs everywhere;
is friendly & easy to learn;
is Open.

当在 Windows 中单独安装 Python 3 使用 `python` 作为命令即可.

而在 Linux 中单独安装 Python 3 要严格使用 `python3` 作为命令.

当安装有多个版本的 Python 时, python3-pip 和 python3-venv 建议用 `python3 -m` 指定 Python 解释器.

```
python3 -m pip
python3 -m venv
```

## 1. install

### 1.1. Debian

```
apt install -y python3 python3-pip python3-venv python3-dev
```

### 1.2. Windows

使用管理员权限安装并添加到环境变量

![使用管理员权限安装并添加到环境变量](./../../../../../images/Python/%E4%BD%BF%E7%94%A8%E7%AE%A1%E7%90%86%E5%91%98%E6%9D%83%E9%99%90%E5%AE%89%E8%A3%85%E5%B9%B6%E6%B7%BB%E5%8A%A0%E5%88%B0%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F.png)

## 2. init

配置镜像加速

```
python3 -m pip config set global.index-url "https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple"
```

## 3. use

> 一般情况下， Python 读一行执行一行

### 3.1. 交互模式

> 将命令保存到文件中执行叫做命令行模式，在 pycharm 控制台或 python 终端执行叫做交互模式
>
> 交互模式下无需打印，可直接得到结果

打开 Pycharm 控制台进入交互模式

![打开 Pycharm 控制台进入交互模式](./../../../../../images/Python/%E6%89%93%E5%BC%80%20Pycharm%20%E6%8E%A7%E5%88%B6%E5%8F%B0%E8%BF%9B%E5%85%A5%E4%BA%A4%E4%BA%92%E6%A8%A1%E5%BC%8F.png)

打开 python 终端，进入交互模式

![打开 Python 终端，进入交互模式](./../../../../../images/Python/%E6%89%93%E5%BC%80%20Python%20%E7%BB%88%E7%AB%AF%EF%BC%8C%E8%BF%9B%E5%85%A5%E4%BA%A4%E4%BA%92%E6%A8%A1%E5%BC%8F.png)

终端执行命令，进入交互模式

```powershell
PS C:\Users\sec> python
```

![终端执行命令，进入交互模式](./../../../../../images/Python/%E7%BB%88%E7%AB%AF%E6%89%A7%E8%A1%8C%E5%91%BD%E4%BB%A4%EF%BC%8C%E8%BF%9B%E5%85%A5%E4%BA%A4%E4%BA%92%E6%A8%A1%E5%BC%8F.png)

> 在终端进入的交互模式可执行 `quit()` ，或者 `exit()` 函数退出

## 4. 报错

某些符号需要成对出现 (如: 引号)

```python
print('hello,world")
```

```
SyntaxError: unterminated string literal (detected at line 1)

进程已结束，退出代码为 1
```

使用了无效字符（如: 中文引号）

```python
print(“hello,world”)
```

```
SyntaxError: invalid character '“' (U+201C)

进程已结束，退出代码为 1
```

---

Refrences

- [Python](https://www.python.org/)
- [Python Documentation](https://www.python.org/doc/)
