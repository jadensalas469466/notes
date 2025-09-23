XSS Fuzz

## 1. Install

下载

```
┌──(sec@debian)-[~]
└─$ git clone https://github.com/s0md3v/XSStrike.git ~/.local/xsstrike
```

安装依赖

```
┌──(sec@debian)-[~]
└─$ cd ~/.local/xsstrike && pip3 install -r ./requirements.txt --break-system-packages
```

编写运行脚本

```
┌──(sec@debian)-[~/.local/xsstrike]
└─$ nano ./xsstrike.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 xsstrike
python3 ./xsstrike.py "$@"
```

```
┌──(sec@debian)-[~/.local/xsstrike]
└─$ cat << 'EOF' > ./xsstrike.sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 xsstrike
python3 ./xsstrike.py "$@"
EOF
```

创建链接

```
┌──(sec@debian)-[~/.local/xsstrike]
└─$ chmod +x ./xsstrike.sh && ln -sf ~/.local/xsstrike/xsstrike.sh ~/.local/bin/xsstrike
```

## 2. Usage

测试 GET 传参的网页

```
┌──(root㉿kali-23)-[~]
└─# xsstrike -u "http://example.com/search.php?q=query"
```

测试 POST 传参的网页

```
┌──(root㉿kali-23)-[~]
└─# xsstrike -u "http://example.com/search.php" --data "q=query"
```

---

References

- [XSStrike](https://github.com/s0md3v/XSStrike)
