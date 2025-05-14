Python 的包管理工具.

## 1 安装

安装

```shell
root@debian:~# apt install -y python3-pip
```

## 2 初始化

配置代理


```shell
root@debian:~# python3 -m pip config set global.proxy "http://192.168.1.201:10808"
```

## 3 使用

运行 `pip` 命令

```shell
root@debian:~# python3 -m pip <pip-arguments>
```

### 3.1 Packages

列出所有 Packages

```shell
root@debian:~# python3 -m pipx list
```

安装 Packages

```shell
root@debian:~# python3 -m pip install SomePackage          # 最新版本
root@debian:~# python3 -m pip install SomePackage==1.0.4   # 指定版本
root@debian:~# python3 -m pip install 'SomePackage>=1.0.4' # 最低版本
```

卸载 Packages

```shell
root@debian:~# python3 -m pip uninstall SomePackage
```

### 3.2 Requirements Files

将所有 Packages 导出到 Requirements Files

```shell
root@debian:~# python3 -m pip freeze > requirements.txt
```

从 Requirements Files 中安装

```shell
root@debian:~# python3 -m pip install -r requirements.txt
```

从 Requirements Files 中卸载

```shell
root@debian:~# python3 -m pip uninstall -r requirements.txt --yes
```

### 3.3 Config

列出所有配置

```shell
root@debian:~# python3 -m pip config list
```

配置源

```shell
root@debian:~# python3 -m pip config set global.index-url https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple
```

删除源

```shell
root@debian:~# python3 -m pip config unset global.index-url
```

配置代理

```shell
root@debian:~# python3 -m pip config set global.proxy "http://192.168.1.201:10808"
```

删除代理

```shell
root@debian:~# python3 -m pip config unset global.proxy
```

---

Refrences

- [pip](https://pip.pypa.io/en/stable/)
