Fast passive subdomain enumeration tool.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
```

## 2. Usage

更新

```
┌──(nemo@debian)-[~]
└─$ subfinder -up
```

指定域名扫描

```
┌──(nemo@debian)-[~]
└─$ subfinder -d example.com
```

指定文件扫描

```
┌──(nemo@debian)-[~]
└─$ subfinder -dL ~/domain.txt
```

保存到文件

```
┌──(nemo@debian)-[~]
└─$ subfinder -d example.com -o ~/subfinder_example.com.txt
```

仅显示活跃的 HOST

```
┌──(nemo@debian)-[~]
└─$ subfinder -d example.com -nW
```

仅保存活跃的 HOST

```
┌──(nemo@debian)-[~]
└─$ subfinder -d example.com -nW -o ~/subfinder_example.com.txt
```

查看 API 配置

```
┌──(nemo@debian)-[~]
└─$ subfinder -ls
```

配置 API

```
┌──(nemo@debian)-[~]
└─$ nano ~/.config/subfinder/provider-config.yaml
```

---

References

- [subfinder](https://github.com/projectdiscovery/subfinder)

