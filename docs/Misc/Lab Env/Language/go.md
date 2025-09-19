Build simple, secure, scalable systems with Go.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ curl -fsSL https://github.com/jadensalas469466/script/raw/main/go_install.sh | bash
```

加载环境变量

```
┌──(nemo@debian)-[~]
└─$ source ~/.zshrc
```

## 2. Init

配置镜像加速

```
┌──(nemo@debian)-[~]
└─$ go env -w GOPROXY="https://proxy.golang.org,direct"
```

## 3. Usage

查看配置

```
┌──(nemo@debian)-[~]
└─$ go env
```

创建项目 `~/path/main.go` 

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}

```

> 使用 Visual Studio Code 打开后安装相关插件 Go 和 Code Runner

---

References

- [Go](https://go.dev/)

