A next-generation crawling and spidering framework.

## 1. install

安装

```
go install github.com/projectdiscovery/katana/cmd/katana@latest
```

## 2. use

对单个目标进行爬虫

```
katana -u http://example.com -o katana_example.com.txt
```

对多个目标进行爬虫

```
katana -list url.txt -o katana_url.txt
```

---

Refrences

- [katana](https://github.com/projectdiscovery/katana)
