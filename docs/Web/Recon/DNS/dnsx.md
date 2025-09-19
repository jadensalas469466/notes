dnsx is a fast and multi-purpose DNS toolkit allow to run multiple DNS queries of your choice with a list of user-supplied resolvers.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ go install -v github.com/projectdiscovery/dnsx/cmd/dnsx@latest
```

## 2. Usage

更新

```
┌──(nemo@debian)-[~]
└─$ dnsx -up
```

查询 A 记录

```
┌──(nemo@debian)-[~]
└─$ echo example.com | dnsx -a -ro
```

保存 A 记录

```
┌──(nemo@debian)-[~]
└─$ echo example.com | dnsx -a -ro -o ~/dnsx_example.com.txt
```

查询 PTR 记录

```
┌──(nemo@debian)-[~]
└─$ echo 1.1.1.1 | dnsx -ptr -ro
```

---

References

- [dnsx](https://github.com/projectdiscovery/dnsx)

