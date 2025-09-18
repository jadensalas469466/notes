A utility to detect various technology for a given IP address.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ go install -v github.com/projectdiscovery/cdncheck/cmd/cdncheck@latest
```

## 2. Usage

确认 IP 是否使用了 CDN

```
┌──(nemo@debian)-[~]
└─$ cdncheck -i 1.1.1.1 -cdn
```

显示列表中使用了 CDN 的 IP

```
┌──(nemo@debian)-[~]
└─$ cdncheck -i ./dnsx_example.com.txt -cdn
```

保存列表中使用了 CDN 的 IP

```
┌──(nemo@debian)-[~]
└─$ cdncheck -i ./dnsx_example.com.txt -cdn -o ./cdncheck_example.com.txt
```

---

References

- [cdncheck](https://github.com/projectdiscovery/cdncheck)

