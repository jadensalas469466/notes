依赖于 python-pip 和 virtualenv ，在安装 Packages 时将自动创建 Python 虚拟环境，推荐在简单的运行环境下使用。

可以像 python-pip 一样直接从 Requirements Files 中批量安装，生成类似的 Pipfile ，弥补了 pipx 的不足，并且加入了 Pipfile.lock 用于记录具体的依赖版本。

在安装了多个版本 Python 的复杂环境下要指定 Python 解析器使用:  `python3.7 -m pipenv` 。

---

参考链接

- [Pipenv](https://pipenv.pypa.io/en/latest/)