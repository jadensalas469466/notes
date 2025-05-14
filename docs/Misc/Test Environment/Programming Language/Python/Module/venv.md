用于手动创建独立 python 虚拟环境的工具, 推荐在简单的运行环境下使用.

## 1. 使用

**Debian**

创建虚拟环境

```
python3 -m venv ./venv
```

激活虚拟环境

```
source ./venv/bin/activate
```

退出虚拟环境

```
deactivate
```

**Windows**

创建虚拟环境

```
python -m venv .\venv
```

激活虚拟环境

```
.\venv\Scripts\Activate.ps1
```

退出虚拟环境

```
deactivate
```

---

Refrences

- [venv](https://docs.python3.org/zh-cn/3.13/library/venv.html)

