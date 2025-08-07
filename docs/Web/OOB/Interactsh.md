An OOB interaction gathering server and client library

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ go install -v github.com/projectdiscovery/interactsh/cmd/interactsh-client@latest
```

配置 PDCP_API_KEY

> Get api key at [https://cloud.projectdiscovery.io](https://cloud.projectdiscovery.io/)

```
┌──(sec@debian)-[~]
└─$ interactsh-client -auth
```

## 2. Usage

Verbose Mode

```
┌──(sec@debian)-[~]
└─$ interactsh-client -v -o interactsh.log
```

后台运行 Verbose Mode

```
┌──(sec@debian)-[~]
└─$ nohup interactsh-client -v > ~/nohup.log 2>&1 & echo $! > ~/pid.log
```

仅显示 HTTP 交互

```
┌──(sec@debian)-[~]
└─$ nohup interactsh-client -http-only -v > ~/nohup.log 2>&1 & echo $! > ~/pid.log
```

---

References

- [Interactsh](https://github.com/projectdiscovery/interactsh)