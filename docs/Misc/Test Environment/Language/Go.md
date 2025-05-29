Build simple, secure, scalable systems with Go.

## 1. Install

安装

```
curl -fsSL https://github.com/jadensalas469466/scripts/raw/main/go_install.sh | sh
```

加载环境变量

```
source ~/.zshrc
```

## 2. Init

配置镜像加速

```
go env -w GOPROXY="https://proxy.golang.org,direct"
```

## 3. Usage

查看配置

```
go env
```

创建项目 `~/go/main.go` 

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}

```

> 使用 vscode 打开后安装相关插件 Go 和 Code Runner

---

Refrences

- [Go](https://go.dev/)
- [Go Documentation](https://go.dev/doc/)

