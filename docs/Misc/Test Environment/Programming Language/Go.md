Build simple, secure, scalable systems with Go.

## 1. install

安装

```
bash -c "$(curl -fsSL https://github.com/jadensalas469466/tools/raw/main/other/go_install.sh)"
```

配置环境变量

```
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.zshrc \
&& echo 'export GOPATH=/root/tools/apps/go' >> ~/.zshrc \
&& echo 'export GOBIN=$GOPATH/bin' >> ~/.zshrc \
&& echo 'export PATH=$PATH:$GOBIN' >> ~/.zshrc \
&& source ~/.zshrc \
&& go version
```

## 2. init

配置代理

```
go env -w GOPROXY='https://goproxy.cn,direct'
```

## 3. use

创建项目 `D:\share\code\go\main.go` 

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}

```

> 使用 vscode 打开后安装相关插件 Go 和 Code Runner

配置源

```shell
┌──(root㉿kali)-[~]
└─# go env -w GO111MODULE=on && go env -w GOPROXY=https://goproxy.cn,direct
```

查看源

```shell
┌──(root㉿a-kali-23)-[~]
└─# go env
```

添加至环境变量

```shell
┌──(root㉿a-kali-23)-[~]
└─# echo 'export PATH=$PATH:/root/go/bin' >> ~/.zshrc && source ~/.zshrc
```

配置代理

```shell
┌──(root㉿kali)-[~]
└─# vim ~/.zshrc && source ~/.zshrc
```

```
237 export GOPROXY=socks5://127.0.0.1:10808,direct
```

查看代理

```shell
┌──(root㉿kali)-[~]
└─# echo $GOPROXY
```

---

Refrences

- [Go](https://go.dev/)
- [Go Documentation](https://go.dev/doc/)

