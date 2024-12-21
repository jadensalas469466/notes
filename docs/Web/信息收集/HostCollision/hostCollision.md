一款 Host 碰撞工具.

## 1. 安装

克隆仓库

```shell
root@debian:~# git clone https://github.com/alwaystest18/hostCollision.git /root/tools/hostCollision && cd /root/tools/hostCollision
```

```shell
root@debian:~/tools/hostCollision# go install && go build hostCollision.go
```

## 2. 使用

测试 Host 碰撞

```shell
root@debian:~# hostCollision -df fileName.txt -uf fileName.txt -o fileName.txt
```

---

参考链接

- [hostCollision](https://github.com/alwaystest18/hostCollision)

