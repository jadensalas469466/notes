批量查询 IP 对应域名、备案信息、百度权重。

## 1 部署

下载

```shell
┌──(root㉿kali)-[~]
└─# git clone https://github.com/Sma11New/ip2domain.git /root/tools/ip2domain
```

创建虚拟环境

```shell
┌──(root㉿kali)-[~]
└─# virtualenv /root/tools/ip2domain/venv
```

启用虚拟环境

```shell
┌──(root㉿kali)-[~]
└─# source /root/tools/ip2domain/venv/bin/activate
```

在虚拟环境中安装依赖

```shell
┌──(venv)─(root㉿kali)-[~]
└─# pip install tldextract && pip install -r /root/tools/ip2domain/requirements.txt
```

退出虚拟环境

```shell
┌──(venv)─(root㉿kali)-[~]
└─# deactivate
```

编写脚本

```shell
┌──(root㉿kali)-[~]
└─# vim /root/tools/ip2domain/ip2domain.sh
```

```sh
#!/usr/bin/zsh

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 开启虚拟环境
source /root/tools/ip2domain/venv/bin/activate

# 运行 ip2domain
python3 ip2domain.py "$@"

# 退出虚拟环境
deactivate
```

创建链接

```shell
┌──(root㉿kali)-[~]
└─# chmod +x /root/tools/ip2domain/ip2domain.sh && ln -s /root/tools/ip2domain/ip2domain.sh /usr/local/bin/ip2domain
```

## 2 使用

查看帮助

```shell
┌──(root㉿kali)-[~]
└─# ip2domain -h
```

对目标进行查询

```shell
┌──(root㉿kali)-[~]
└─# ip2domain -t [ip/domain]
```

---

参考链接

- [ip2domain](https://github.com/Sma11New/ip2domain)
