A fast port scanner written in go with a focus on reliability and simplicity. Designed to be used in combination with other tools for attack surface discovery in bug bounties and pentests.

## 1. Install

安装

```
go install -v github.com/projectdiscovery/naabu/v2/cmd/naabu@latest
```

## 2. Usage

扫描 Top 1000 端口开放的目标

```
naabu -l host.txt -tp 1000 -o naabu_host.txt
```

---

Refrences

- [naabu](https://github.com/projectdiscovery/naabu)

