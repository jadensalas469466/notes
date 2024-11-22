信息收集自动化工具。

## 1 部署

[配置 Docker 容器引擎](https://keithpeck177271.gitbook.io/notes/misc/shi-yan-huan-jing/rong-qi/yin-qing/pei-zhi-docker-rong-qi-yin-qing)

添加别名

```shell
root@debian.attack:~# vim ~/.bshrc
```

```
15 alias shuize='docker run --rm -it -v $(pwd)/iniFile:/ShuiZe_0x727/iniFile -v $(pwd)/result:/ShuiZe_0x727/result --name shuize 1itt1eb0y/shuize:latest'
```

重新加载 `~/.bashrc` 文件，使配置生效

```shell
root@debian.attack:~# source ~/.bashrc
```

查看使用帮助

```shell
root@debian.attack:~# shuize -h
```

