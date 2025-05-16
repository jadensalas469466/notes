Build simple, secure, scalable systems with Go.

## 1. install

安装

```
bash -c "$(curl -fsSL https://github.com/jadensalas469466/tools/raw/main/other/go_install.sh)"
```

配置环境变量

```
cat << 'EOF' >> ~/.zshrc

# go env
export PATH=$PATH:/usr/local/go/bin
export GOPATH=$HOME/go
export GOBIN=$GOPATH/bin
export PATH=$PATH:$GOBIN

EOF

source ~/.zshrc
```

## 2. init

配置镜像加速

```
go env -w GOPROXY="https://proxy.golang.org,direct"
```

## 3. use

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

