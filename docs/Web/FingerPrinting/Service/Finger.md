Web 服务指纹识别工具.

## 1. 安装

克隆仓库

```
┌──(root@debian)-[~]
└─# git clone https://github.com/EASY233/Finger.git /root/tools/apps/finger \
&& cd /root/tools/apps/finger
```

激活虚拟环境

```
┌──(root@debian)-[~/tools/apps/finger]
└─# python3 -m venv ./venv \
&& source ./venv/bin/activate
```

安装依赖

```
┌──(venv)─(root@debian)-[~/tools/apps/finger]
└─# python3 -m pip install -r ./requirements.txt
```

查看帮助

```
┌──(venv)─(root@debian)-[~/tools/apps/finger]
└─# python3 ./Finger.py -h
```

退出虚拟环境

```
┌──(venv)─(root@debian)-[~/tools/apps/finger]
└─# deactivate
```

## 2. 初始化

编写运行脚本

```
┌──(root@debian)-[~/tools/apps/finger]
└─# nano ./finger.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 激活虚拟环境
source /root/tools/apps/finger/venv/bin/activate

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 finger
python3 Finger.py "$@"
```

创建链接

```
┌──(root@debian)-[~/tools/apps/finger]
└─# chmod +x ./finger.sh \
&& ln -s /root/tools/apps/finger/finger.sh /usr/local/bin/finger \
&& cd
```

查看帮助

```
┌──(root@debian)-[~]
└─# finger -h
```

## 3. 使用

识别目标使用的 Web 服务

```
finger -u https://example.com -o json
```

查看结果

```
ls /root/tools/apps/finger/output/
```

---

参考链接

- [Finger](https://github.com/EASY233/Finger)
