## 部署

安装

```shell
┌──(root㉿kali)-[~]
└─# apt install -y golang-go
```

## 初始化

配置源

```shell
┌──(root㉿kali)-[~]
└─# go env -w GO111MODULE=on && go env -w GOPROXY=https://goproxy.cn,direct
```

添加至环境变量

```shell
┌──(root㉿a-kali-23)-[~]
└─# echo 'export PATH=$PATH:/root/go/bin' >> ~/.zshrc && source ~/.zshrc
```

## 使用

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

参考链接

- [Go](https://go.dev/)

