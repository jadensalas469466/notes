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
└─$ katana -u http://example.com -e cdn,private-ips -o katana_example.com.txt
```

对多个目标进行爬虫

```
┌──(sec@debian)-[~]
└─$ katana -list url.txt -e cdn,private-ips -o katana_url.txt
```

爬取 JS

```
┌──(sec@debian)-[~]
└─$ katana -list url.txt -jc -e cdn,private-ips -o katana_url.txt
```

---

Refrences

- [katana](https://github.com/projectdiscovery/katana)
