A fast port scanner written in go with a focus on reliability and simplicity. Designed to be used in combination with other tools for attack surface discovery in bug bounties and pentests.

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ go install -v github.com/projectdiscovery/naabu/v2/cmd/naabu@latest
```

## 2. Init

创建软链接以全局运行

```
┌──(sec@debian)-[~]
└─$ sudo ln -sf ~/.local/bin/naabu /usr/local/bin/naabu
```

## 3. Usage

扫描常见的 Web 端口

```
┌──(sec@debian)-[~]
└─$ sudo naabu -host example.com -Pn -o ~/naabu_example.com.txt
```

---

References

- [naabu](https://github.com/projectdiscovery/naabu)

