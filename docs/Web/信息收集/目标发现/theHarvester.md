综合信息收集工具。

# 1 部署

配置 `api` 

```shell
┌──(root㉿kali)-[~]
└─# vim /etc/theHarvester/api-keys.yaml
```

```yaml
54 shodan:
55 key:YQchKbHxjEgzXUqoR1qbtxec79P23owU
```

# 2 使用

查看帮助

```shell
┌──(root㉿kali)-[~]
└─# theHarvester -h
```

# 3 实战

调用 `duckduckgo` 对目标进行信息搜集

```shell
┌──(root㉿kali)-[~]
└─# proxychains4 theHarvester -d [domain] -b duckduckgo
```

调用 `shodan` 对目标进行信息搜集

```shell
┌──(root㉿kali)-[~]
└─# proxychains4 theHarvester -d [domain] -s
```

---

参考连接

- [theHarvester](https://github.com/laramies/theHarvester)
