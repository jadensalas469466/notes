一个简化的防火墙管理工具。

# 1 部署

安装

```shell
┌──(root㉿a-kali-23)-[~]
└─# sudo apt install -y ufw 
```

# 2 使用

查看使用帮助

```shell
┌──(root㉿a-kali-23)-[~]
└─# ufw -h
```

```
Usage: ufw COMMAND

Commands:
 enable                          启用防火墙
 disable                         禁用防火墙
 default ARG                     设置默认策略
 logging LEVEL                   将日志记录设置为 LEVEL
 allow ARGS                      添加允许规则
 deny ARGS                       添加拒绝规则
 reject ARGS                     添加拒绝规则
 limit ARGS                      添加限制规则
 delete RULE|NUM                 删除规则
 insert NUM RULE                 在 NUM 处插入规则
 prepend RULE                    预置规则
 route RULE                      添加路由规则
 route delete RULE|NUM           删除路线规则
 route insert NUM RULE           在 NUM 处插入路由规则
 reload                          重启防火墙
 reset                           重置防火墙
 status                          显示防火墙规则
 status numbered                 以规则编号列表的形式显示防火墙状态
 status verbose                  显示防火墙状态
 show ARG                        显示防火墙状态
 version                         显示版本信息

Application profile commands:
 app list                        列出应用程序配置文件
 app info PROFILE                显示配置文件的信息
 app update PROFILE              更新配置文件
 app default ARG                 设置默认应用程序策略
```

---

参考链接

- [UFW](https://github.com/jbq/ufw)
