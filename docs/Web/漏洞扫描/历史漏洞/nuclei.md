Web 漏洞 POC 扫描工具。

## 1 安装

安装

```shell
┌──(root㉿kali)-[~]
└─# sudo apt install -y nuclei
```

## 2 使用

查看帮助

```shell
┌──(root㉿kali)-[~]
└─# nuclei -h
```

对目标进行漏洞扫描

```shell
┌──(root㉿kali)-[~]
└─# nuclei -u [url]
```

## 3 帮助

```shell
┌──(root㉿kali-23)-[~]
└─# nuclei -h
```

```
Nuclei 是一个快速、基于模板的漏洞扫描器，专注于广泛的可配置性、巨大的可扩展性和易用性。

使用方法:
  nuclei [标志]

标志:
目标:
   -u, -target string[]          要扫描的目标 URLs/主机
   -l, -list string              包含要扫描的目标 URLs/主机列表的文件路径（一行一个）
   -eh, -exclude-hosts string[]  从输入列表中排除要扫描的主机（IP，CIDR，主机名）
   -resume string                使用 resume.cfg 恢复扫描（将禁用聚类）
   -sa, -scan-all-ips            扫描与 DNS 记录关联的所有 IP
   -iv, -ip-version string[]     要扫描的主机名的 IP 版本 (4,6) -（默认 4）

目标格式:
   -im, -input-mode string        输入文件的模式（list, burp, jsonl, yaml, openapi, swagger）（默认 "list"）
   -ro, -required-only            生成请求时仅使用输入格式中必需的字段
   -sfv, -skip-format-validation  解析输入文件时跳过格式验证（如缺少变量）

模板:
   -nt, -new-templates                    仅运行在最新 nuclei-templates 版本中添加的新模板
   -ntv, -new-templates-version string[]  运行在特定版本中添加的新模板
   -as, -automatic-scan                   使用 wappalyzer 技术检测映射到标签的自动化 Web 扫描
   -t, -templates string[]                要运行的模板或模板目录列表（逗号分隔，文件）
   -turl, -template-url string[]          要运行的模板 URL 或包含模板 URL 的列表（逗号分隔，文件）
   -w, -workflows string[]                要运行的工作流或工作流目录列表（逗号分隔，文件）
   -wurl, -workflow-url string[]          要运行的工作流 URL 或包含工作流 URL 的列表（逗号分隔，文件）
   -validate                              验证传递给 nuclei 的模板
   -nss, -no-strict-syntax                禁用模板的严格语法检查
   -td, -template-display                 显示模板内容
   -tl                                    列出所有可用的模板
   -tgl                                   列出所有可用的标签
   -sign                                  使用 NUCLEI_SIGNATURE_PRIVATE_KEY 环境变量中定义的私钥签署模板
   -code                                  启用加载基于代码协议的模板
   -dut, -disable-unsigned-templates      禁止运行未签名的模板或签名不匹配的模板

过滤:
   -a, -author string[]               基于作者运行模板（逗号分隔，文件）
   -tags string[]                     基于标签运行模板（逗号分隔，文件）
   -etags, -exclude-tags string[]     基于标签排除模板（逗号分隔，文件）
   -itags, -include-tags string[]     即使默认或配置排除，也要执行的标签
   -id, -template-id string[]         基于模板 ID 运行模板（逗号分隔，文件，允许通配符）
   -eid, -exclude-id string[]         基于模板 ID 排除模板（逗号分隔，文件）
   -it, -include-templates string[]   即使默认或配置排除，也要执行的模板文件或目录路径
   -et, -exclude-templates string[]   排除的模板文件或目录路径（逗号分隔，文件）
   -em, -exclude-matchers string[]    在结果中排除的模板匹配器
   -s, -severity value[]              基于严重性运行模板。可能的值：info, low, medium, high, critical, unknown
   -es, -exclude-severity value[]     基于严重性排除模板。可能的值：info, low, medium, high, critical, unknown
   -pt, -type value[]                 基于协议类型运行模板。可能的值：dns, file, http, headless, tcp, workflow, ssl, websocket, whois, code, javascript
   -ept, -exclude-type value[]        基于协议类型排除模板。可能的值：dns, file, http, headless, tcp, workflow, ssl, websocket, whois, code, javascript
   -tc, -template-condition string[]  基于表达式条件运行模板

输出:
   -o, -output string            写入发现问题/漏洞的输出文件
   -sresp, -store-resp           将通过 nuclei 的所有请求/响应存储到输出目录
   -srd, -store-resp-dir string  将通过 nuclei 的所有请求/响应存储到自定义目录（默认 "output"）
   -silent                       仅显示发现的结果
   -nc, -no-color                禁用输出内容的着色（ANSI 转义码）
   -j, -jsonl                    以 JSONL(ines) 格式写入输出
   -irr, -include-rr -omit-raw   在 JSON、JSONL 和 Markdown 输出中包含请求/响应对（仅发现）【已弃用，请使用 -omit-raw】（默认 true）
   -or, -omit-raw                在 JSON、JSONL 输出中省略请求/响应对（仅发现）
   -ot, -omit-template           在 JSON、JSONL 输出中省略编码的模板
   -nm, -no-meta                 禁用在 CLI 输出中打印结果元数据
   -ts, -timestamp               启用在 CLI 输出中打印时间戳
   -rdb, -report-db string       nuclei 报告数据库（始终使用此选项持久化报告数据）
   -ms, -matcher-status          显示匹配失败状态
   -me, -markdown-export string  导出结果到 Markdown 格式的目录
   -se, -sarif-export string     导出结果到 SARIF 格式的文件
   -je, -json-export string      导出结果到 JSON 格式的文件
   -jle, -jsonl-export string    导出结果到 JSONL(ine) 格式的文件

配置:
   -config string                        nuclei 配置文件的路径
   -tp, -profile string                  要运行的模板配置文件
   -tpl, -profile-list                   列出社区模板配置文件
   -fr, -follow-redirects                启用 HTTP 模板的重定向跟随
   -fhr, -follow-host-redirects          跟随同一主机的重定向
   -mr, -max-redirects int               要跟随的 HTTP 模板最大重定向次数（默认 10）
   -dr, -disable-redirects               禁用 HTTP 模板的重定向
   -rc, -report-config string            nuclei 报告模块配置文件
   -H, -header string[]                  在所有 HTTP 请求中包含自定义头/COOKIE，格式为 header:value（CLI，文件）
   -V, -var value                        以 key=value 格式的自定义变量
   -r, -resolvers string                 包含解析器列表的文件
   -sr, -system-resolvers                使用系统 DNS 解析作为错误后备
   -dc, -disable-clustering              禁用请求的聚类
   -passive                              启用被动 HTTP 响应处理模式
   -fh2, -force-http2                    强制请求使用 HTTP2 连接
   -ev, -env-vars                        启用在模板中使用环境变量
   -cc, -client-cert string              用于认证扫描主机的客户端证书文件（PEM 编码）
   -ck, -client-key string               用于认证扫描主机的客户端密钥文件（PEM 编码）
   -ca, -client-ca string                用于认证扫描主机的客户端证书颁发机构文件（PEM 编码）
   -sml, -show-match-line                显示文件模板的匹配行，仅适用于提取器
   -ztls                                 使用 ztls 库，并自动回退到标准的 TLS13【已弃用】默认启用自动回退到 ztls
   -sni string                           要使用的 TLS SNI 主机名（默认：输入域名）
   -dt, -dialer-timeout value            网络请求的超时时间
   -dka, -dialer-keep-alive value        网络请求的保持连接时间
   -lfa, -allow-local-file-access        允许系统上任何地方的文件（有效载荷）访问
   -lna, -restrict-local-network-access  阻止连接到本地/私人网络
   -i, -interface string                 用于网络扫描的网络接口
   -at, -attack-type string              要执行的有效载荷组合类型（batteringram, pitchfork, clusterbomb）
   -sip, -source-ip string               使用特定的源 IP 地址
   -rate int                             每秒请求速率限制
   -rl, -rate-limit int                  每秒请求速率限制
   -rw, -report-webhook string           检测到时发送到此 URL 的 webhook
   -sl, -stats-log string                日志文件以接收统计信息
   -mwu, -markdown-update string         发送更新时的 Webhook URL
   -mwd, -markdown-directory string      用于接收 Webhook 的 Markdown 目录
```

---

参考链接

- [nuclei](https://www.kali.org/tools/nuclei/)

