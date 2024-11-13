Python 的包管理工具。

# 1 初始化

配置源

```shell
┌──(root㉿kali-23)-[~]
└─# pip config set global.index-url https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple
```

# 2 使用

安装软件

```shell
┌──(root㉿kali)-[~]
└─# pip install virtualenv
```

安装依赖

```shell
┌──(root㉿kali)-[~]
└─# pip install -r requirements.txt
```

卸载依赖

```shell
┌──(root㉿kali)-[~]
└─# pip uninstall -r -y requirements.txt
```

配置源

```shell
┌──(root㉿kali-23)-[~]
└─# pip config set global.index-url https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple
```

删除源

```shell
┌──(root㉿kali-23)-[~]
└─# pip config unset global.index-url
```

配置代理

```shell
┌──(root㉿kali)-[~]
└─# pip config set global.proxy "socks5://127.0.0.1:10808"
```

查看代理

```shell
┌──(root㉿kali)-[~]
└─# pip config list
```

```
global.proxy='socks5://127.0.0.1:10808'
```

---

参考链接

- [PyPI](https://pypi.org/)
