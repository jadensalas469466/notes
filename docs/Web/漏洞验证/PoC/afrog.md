Web 漏洞 PoC 扫描工具.

## 1. 安装

克隆仓库

```
┌──(root@debian)-[~]
└─# git clone https://github.com/zan8in/afrog.git /root/tools/apps/afrog \
&& cd /root/tools/apps/afrog
```

安装

```
┌──(root@debian)-[~/tools/apps/afrog]
└─# go build ./cmd/afrog/main.go
```

查看帮助

```
┌──(root@debian)-[~/tools/apps/afrog]
└─# ./main -h
```

## 2. 初始化

修改配置文件

```
┌──(root@debian)-[~/tools/apps/afrog]
└─# vim /root/.config/afrog/afrog-config.yaml
```

```yaml
server: :16868
reverse:
  alphalog:
    domain: ""
    api_url: ""
  ceye:
    api-key: ""
    domain: ""
  dnslogcn:
    domain: dnslog.cn
  eye:
    host: ""
    token: ""
    domain: ""
  jndi:
    jndi_address: ""
    ldap_port: ""
    api_port: ""
  xray:
    x_token: ""
    domain: ""
    api_url: http://x.x.x.x:8777
  revsuit:
    token: ""
    dns_domain: ""
    http_url: ""
    api_url: ""
webhook:
  dingtalk:
```

编写运行脚本

```
┌──(root@debian)-[~/tools/apps/afrog]
└─# vim ./afrog.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 afrog
./main "$@"
```

创建链接

```
┌──(root@debian)-[~/tools/apps/afrog]
└─# chmod +x ./afrog.sh && ln -s /root/tools/apps/afrog/afrog.sh /usr/local/bin/afrog && cd
```

查看帮助

```
┌──(root@debian)-[~]
└─# afrog -h
```

## 3. 使用

扫描 PoC

```
afrog -t https://example.com -o /root/fileName.html
```

