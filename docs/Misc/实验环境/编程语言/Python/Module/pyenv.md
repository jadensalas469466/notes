Python 多版本管理工具.

## 1. 安装

安装依赖

```
┌──(root@debian)-[~]
└─# apt update && apt install -y build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev curl git \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
```

安装主程序

```
┌──(root@debian)-[~]
└─# curl https://pyenv.run | bash
```

## 2. 初始化

设置环境变量

```
┌──(root@debian)-[~]
└─# vim ~/.zshrc && source ~/.zshrc
```

```
# Shell environment for pyenv
    export PYENV_ROOT="$HOME/.pyenv"
    [[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
    eval "$(pyenv init -)"
```

## 3. 使用

安装指定的 Python 版本

```
┌──(root@debian)-[~]
└─# pyenv install <version> # For example: pyenv install 3.6
```

刷新 shim

```
┌──(root@debian)-[~]
└─# pyenv rehash
```

设置当前目录的 Python 版本

```
┌──(root@debian)-[~]
└─# pyenv local <version>
```

指定 Python 版本执行

```
┌──(root@debian)-[~]
└─# pyenv exec python<version>
```

## 4. 帮助

version

```
pyenv version  # 查看当前使用的 Python 版本
pyenv versions # 查看所有已安装的 Python 版本
```

install

```
pyenv install -l        # 列出所有可安装的 Python 版本
pyenv install <version> # 安装指定的 Python 版本
```

shim

```
pyenv shims  # 列出现有的 pyenv shim
pyenv rehash # 刷新 pyenv shim (安装可执行文件后运行此命令)
```

uninstall

```
pyenv uninstall <version> # 卸载指定的 Python 版本
```

exec

```
pyenv exec python<version> # 指定 Python 版本执行
```

global

```
pyenv global           # 查看当前全局设置的 Python 版本
pyenv global <version> # 全局设置 Python 版本
pyenv global system    # 恢复全局设置为默认的 Python 的版本
```

shell

```
pyenv shell <version> # 临时全局设置 Python 版本
pyenv shell --unset   # 取消临时全局设置
```

local

```
pyenv local <version> # 设置当前目录的 Python 版本
pyenv local --unset   # 取消当前目录设置
```

---

参考链接

- [Pyenv](https://github.com/pyenv/pyenv#installation)

