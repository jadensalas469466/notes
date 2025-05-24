httpx is a fast and multi-purpose HTTP toolkit that allows running multiple probes using the retryablehttp library.

## 1. install

安装

```
go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest
```

## 2. use

检测存活的站点

```
httpx -l host.txt -o httpx_url.txt
```

---

Refrences

- [httpx](https://github.com/projectdiscovery/httpx)

