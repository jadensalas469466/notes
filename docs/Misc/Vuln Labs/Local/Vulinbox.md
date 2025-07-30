## 1. Install

复制下载地址

![复制下载地址](./../../../../images/Vulinbox/%E5%A4%8D%E5%88%B6%E4%B8%8B%E8%BD%BD%E5%9C%B0%E5%9D%80.png)

下载

```
┌──(root@debian)-[~]
└─# mkdir /root/tools/apps/vulinbox && cd /root/tools/apps/vulinbox && curl -LO https://oss-qn.yaklang.com/vulinbox/latest/vulinbox_linux_amd64
```

编写运行脚本

```
┌──(root@debian)-[~/tools/apps/vulinbox]
└─# chmod +x ./vulinbox_linux_amd64 && vim ./vulinbox.sh
```

```sh
#!/bin/bash

# 错误检测
set -e

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 vulinbox
./vulinbox_linux_amd64 "$@"

```

创建链接

```
┌──(root@debian)-[~/tools/apps/vulinbox]
└─# chmod +x ./vulinbox.sh && ln -s /root/tools/apps/vulinbox/vulinbox.sh /usr/local/bin/vulinbox
```

## 3. Use

```
┌──(root@debian)-[~]
└─# vulinbox
```

> 访问 https://debian.local:8080/

---

References

- [Vulinbox](https://yaklang.io/Yaklab/vulinbox/vulinbox)

