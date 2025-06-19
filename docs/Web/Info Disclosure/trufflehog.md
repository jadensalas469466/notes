Find, verify, and analyze leaked credentials.

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ curl -sSfL https://raw.githubusercontent.com/trufflesecurity/trufflehog/main/scripts/install.sh | sh -s -- -b ~/.local/bin
```

## 2. Usage

### 2.1. 扫描仓库

Scan a repo for only verified secrets

```
┌──(sec@debian)-[~]
└─$ trufflehog git https://github.com/trufflesecurity/test_keys --results=verified,unknown
```

---

Refrences

- [trufflehog](https://github.com/trufflesecurity/trufflehog)