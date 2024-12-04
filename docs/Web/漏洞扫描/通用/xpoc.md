Web 漏洞 POC 扫描工具。

## 1 部署

下载

```shell
┌──(root㉿kali)-[~]
└─# proxychains4 wget https://github.com/chaitin/xpoc/releases/download/0.0.8/xpoc_linux_amd64.zip
```

解压

```shell
┌──(root㉿kali)-[~]
└─# mkdir /root/tools/xpoc && unzip xpoc_linux_amd64.zip -d /root/tools/xpoc && rm -rf xpoc_linux_amd64.zip
```

编写脚本

```shell
┌──(root㉿kali)-[~]
└─# chmod +x /root/tools/xpoc/xpoc_linux_amd64 && vim /root/tools/xpoc/xpoc.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 xpoc
./xpoc_linux_amd64 "$@"
```

创建链接

```shell
┌──(root㉿kali)-[~]
└─# chmod +x /root/tools/xpoc/xpoc.sh && ln -s /root/tools/xpoc/xpoc.sh /usr/local/bin/xpoc
```

同步最新插件

```shell
┌──(root㉿kali)-[~]
└─# xpoc pull
```

## 2 使用

查看帮助

```shell
┌──(root㉿kali)-[~]
└─# xpoc -h
```

```
   __  /\    /\_.  ___.  _____
  | |/ /   / __.\/ __.\/ ____|
  |   /XRAY™/_/ / / / / /
 / . |   / .___/ /_/ / /___.
/ /|_|  / /    \____/\____/
\/v0.0.3\/cloud plugins: [97]

[INFO] 2023-05-26 15:10:17 use config at: xpoc-config.yaml [strategy.go:30]

NAME:
  xpoc - light poc scanner

USAGE:
  Scan single target:      xpoc -t https://example.com
   └>  multiple targets:   xpoc -t 192.168.0.1,192.168.0.1:443,tcp://192.168.1.1:8000
  Input from file:         xpoc -i targets.txt
   └>   from pipe:         cat targets.txt | xpoc
  Output to JSON:          xpoc -t https://example.com -o result.json
   └>    to HTML:          xpoc -t https://example.com -o result.html
  Run plugins form cloud:  xpoc -r 1 -t http://example.com
   └> plugins from local:  xpoc -r ./poc-yaml-example.yaml -t http://example.com
  List local plugins:      xpoc list
   └>  cloud plugins:      xpoc list -a
  Pull all cloud plugins:  xpoc pull
   └>  specific plugins:   xpoc pull -id 1

COMMANDS:
  pull     下载及更新插件
  add      将文件添加到插件仓库
  list     列出插件
  upgrade  升级到最新版本
  help, h  Shows a list of commands or help for one command

GLOBAL OPTIONS:
  --run value, -r value      执行指定插件 多个插件间','分割 支持glob语法 用于测试插件或过滤插件
  --enable value, -e value   在默认策略（全量探测）基础上增加本地插件，支持glob语法
  --disable value, -d value  禁用部分插件，支持glob语法
  --config value, -c value   指定配置文件
  --debug                    debug (default: false)
  --quiet, -q                不显示banner (default: false)
  -p value                   需要探测的TCP端口 <info-live>
  --bw value                 最大带宽占用限制(KB/s): 限制扫描发包的最大速率 与PPS的换算关系为: PPS=带宽*1024/60 <info-live> (default: 2000)
  --Pn                       禁用主机存活探测: 端口扫描之前不进行主机存活探测 <info-live> (default: false)
  -o value [ -o value ]      结果输出: 指定保存结果的文件路径 <result-printer>
  -t value                   扫描目标: 可以为URL/IP/域名/Host:Port等多种形式的混合输入 <util-target-split> <default>
  -i value                   目标文件: 指定含有扫描目标的文本文件 <util-target-split>
  --help, -h                 show help (default: false)
```

扫描指定目标

```shell
┌──(root㉿kali)-[~]
└─# xpoc -t https://example.com -o result.html
```

查看所有云端的POC

```shell
┌──(root㉿kali)-[~]
└─# xpoc list -a
```

批量扫描

```shell
┌──(root㉿kali)-[~]
└─# xpoc < targets.txt
```

```shell
┌──(root㉿kali)-[~]
└─# cat targets.txt | xpoc
```

```shell
┌──(root㉿kali)-[~]
└─# xpoc -i targets.txt
```

同步最新插件

```shell
┌──(root㉿kali)-[~]
└─# xpoc pull
```

更新到最新版本

```shell
┌──(root㉿kali)-[~]
└─# xpoc upgrade
```

---

参考链接

- [xpoc](https://github.com/chaitin/xpoc)
