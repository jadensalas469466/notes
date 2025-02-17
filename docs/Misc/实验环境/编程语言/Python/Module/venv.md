用于手动创建独立 Python 虚拟环境的工具, 推荐在简单的运行环境下使用.

## 1 使用

创建虚拟环境

```
┌──(root@debian)-[~/path]
└─# python -m venv ./venv
```

激活虚拟环境

```
┌──(root@debian)-[~/path]
└─# source ./venv/bin/activate
```

退出虚拟环境

```
┌──(root@debian)-[~/path]
└─# deactivate
```

---

参考链接

- [venv](https://docs.python.org/zh-cn/3.13/library/venv.html)

