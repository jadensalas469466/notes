依赖于 python-pip 和 python-venv, 在独立安装时将自动为每个 Packages 创建单独的虚拟环境.

## 1 安装

安装

```
┌──(root@debian)-[~]
└─# apt install -y pipx
```

## 2 初始化

配置依赖于 `pip` ，无需额外配置

## 3 使用

运行 `pip` 命令

```
┌──(root@debian)-[~]
└─# pipx <pipx-arguments>
```

### 3.1 Packages

列出所有 Packages

```
┌──(root@debian)-[~]
└─# pipx list
```

安装 Packages

```
┌──(root@debian)-[~]
└─# pipx install SomePackage              # 最新版本
┌──(root@debian)-[~]
└─# pipx install SomePackage==1.0.4       # 指定版本
┌──(root@debian)-[~]
└─# pipx install 'SomePackage>=1.0.4'     # 最低版本
┌──(root@debian)-[~]
└─# pipx install --suffix=2.0 SomePackage # 添加后缀安装避免冲突，这里为 SomePackage2.0
```

重装 Packages

```
┌──(root@debian)-[~]
└─# pipx reinstall SomePackage # 指定重装
┌──(root@debian)-[~]
└─# pipx reinstall-all         # 全部重装
```

卸载 Packages

```
└─# pipx uninstall SomePackage # 指定卸载
└─# pipx uninstall-all         # 全部卸载
```

更新 Packages

```
┌──(root@debian)-[~]
└─# pipx upgrade SomePackage # 指定更新
┌──(root@debian)-[~]
└─# pipx upgrade-all         # 全部更新
```

### 3.2 环境变量

链接所有虚拟环境变量到全局环境变量

```
┌──(root@debian)-[~]
└─# pipx ensurepath
```

---

Refrences

- [pipx](https://pipx.pypa.io/stable/)

