依赖于 python-pip 和 python-venv ，在安装 Packages 时将自动创建 Python 虚拟环境，推荐在简单的运行环境下使用。

无法像 python-pip 一样直接从 Requirements Files 中批量安装，但是可以读取 Requirements Files 内容逐个安装。

在安装了多个版本 Python 的复杂环境下要指定 Python 版本使用:  `python3.7 -m pipx` 。

## 1 部署

安装

```shell
root@debian:~# apt install -y pipx
```

## 2 初始化

配置依赖于 `pip` ，无需额外配置

## 3 使用

运行 `pip` 命令

```shell
root@debian:~# python -m pipx <pipx-arguments>
```

### 3.1 Packages

列出所有 Packages

```shell
root@debian:~# python -m pipx list
```

安装 Packages

```shell
root@debian:~# python -m pipx install SomePackage              # 最新版本
root@debian:~# python -m pipx install SomePackage==1.0.4       # 指定版本
root@debian:~# python -m pipx install 'SomePackage>=1.0.4'     # 最低版本
root@debian:~# python -m pipx install --suffix=2.0 SomePackage # 添加后缀安装避免冲突，这里为 SomePackage2.0
```

重装 Packages

```shell
root@debian:~# python -m pipx reinstall SomePackage # 指定重装
root@debian:~# python -m pipx reinstall-all         # 全部重装
```

卸载 Packages

```shell
root@debian:~# python -m pipx uninstall SomePackage # 指定卸载
root@debian:~# python -m pipx uninstall-all         # 全部卸载
```

更新 Packages

```shell
root@debian:~# python -m pipx upgrade SomePackage # 指定更新
root@debian:~# python -m pipx upgrade-all         # 全部更新
```

### 3.2 环境变量

链接所有虚拟环境变量到全局环境变量

```shell
root@debian:~# python -m pipx ensurepath
```

---

参考链接

- [pipx](https://pipx.pypa.io/stable/)

