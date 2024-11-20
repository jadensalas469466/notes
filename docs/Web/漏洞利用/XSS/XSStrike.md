XSS Fuzz。

## 1 部署

下载

```shell
┌──(root㉿kali-23)-[~]
└─# git clone https://github.com/s0md3v/XSStrike.git /root/tools/xsstrike
```

安装

```shell
┌──(root㉿kali-23)-[~]
└─# pip3 install -r /root/tools/xsstrike/requirements.txt
```

编写脚本

```shell
┌──(root㉿kali-23)-[~]
└─# vim /root/tools/xsstrike/xsstrike.sh
```

```sh
#!/usr/bin/zsh

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 xsstrike
python3 xsstrike.py "$@"
```

创建链接

```shell
┌──(root㉿kali)-[~]
└─# chmod +x /root/tools/xsstrike/xsstrike.sh && ln -s /root/tools/xsstrike/xsstrike.sh /usr/local/bin/xsstrike
```

## 2 使用

测试 get 传参的网页

```shell
┌──(root㉿kali-23)-[~]
└─# xsstrike -u '[url?payload=1]' --crawl
```

测试 post 传参的网页

```shell
┌──(root㉿kali-23)-[~]
└─# xsstrike -u '[url]' --data 'payload=1' -d 1
```

## 3 帮助

```shell
┌──(root㉿kali-23)-[~]
└─# xsstrike -h
```

```
XSStrike v3.1.5

用法: xsstrike.py [-h] [-u 目标] [--data 参数数据] [-e 编码] [--fuzzer] [--update] [--timeout 超时] [--proxy] [--crawl] [--json] [--path] [--seeds 参数种子] [-f 参数文件] [-l 级别] [--headers [添加标头]] [-t 线程数] [-d 延迟] [--skip] [--skip-dom] [--blind] [--console-log-level {DEBUG,INFO,RUN,GOOD,WARNING,ERROR,CRITICAL,VULN}] [--file-log-level {DEBUG,INFO,RUN,GOOD,WARNING,ERROR,CRITICAL,VULN}] [--log-file 日志文件]

选项:
  -h, --help            显示此帮助消息并退出
  -u TARGET, --url TARGET
                        URL
  --data PARAMDATA      POST 数据
  -e ENCODE, --encode ENCODE
                        编码有效载荷
  --fuzzer              Fuzzer
  --update              更新
  --timeout TIMEOUT     超时
  --proxy               使用代理
  --crawl               爬行
  --json                将 POST 数据视为 JSON
  --path                在路径中注入有效载荷
  --seeds ARGS_SEEDS    从文件加载爬行种子
  -f ARGS_FILE, --file ARGS_FILE
                        从文件加载有效载荷
  -l LEVEL, --level LEVEL
                        爬行级别
  --headers [ADD_HEADERS]
                        添加标头
  -t THREADCOUNT, --threads THREADCOUNT
                        线程数
  -d DELAY, --delay DELAY
                        请求之间的延迟
  --skip                不要询问是否继续
  --skip-dom            跳过 DOM 检查
  --blind               在爬行时注入盲 XSS 载荷
  --console-log-level {DEBUG,INFO,RUN,GOOD,WARNING,ERROR,CRITICAL,VULN}
                        控制台日志级别
  --file-log-level {DEBUG,INFO,RUN,GOOD,WARNING,ERROR,CRITICAL,VULN}
                        文件日志级别
  --log-file LOG_FILE   要记录的文件名
```

---

参考链接

- [XSStrike](https://github.com/s0md3v/XSStrike)
