A next-generation crawling and spidering framework.

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ go install github.com/projectdiscovery/katana/cmd/katana@latest
```

## 2. Usage

对单个目标进行爬虫

```
┌──(sec@debian)-[~]
└─$ katana -u http://example.com -iqp -e cdn,private-ips -ef css -o katana_example.com.txt
```

对多个目标进行爬虫

```
┌──(sec@debian)-[~]
└─$ katana -list url.txt -iqp -e cdn,private-ips -ef css -o katana_url.txt
```

爬取单个目标的 JS

```
┌──(sec@debian)-[~]
└─$ katana -u http://example.com -jc -iqp -e cdn,private-ips -em js -o katana_example.com-js.txt
```

爬取多个目标的 JS

```
┌──(sec@debian)-[~]
└─$ katana -list url.txt -jc -iqp -e cdn,private-ips -em js -o katana_url-js.txt
```

---

References

- [katana](https://github.com/projectdiscovery/katana)
