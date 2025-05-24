Find, verify, and analyze leaked credentials.

## 1. install

```
curl -sSfL https://raw.githubusercontent.com/trufflesecurity/trufflehog/main/scripts/install.sh | sh -s -- -b /usr/local/bin
```

## 2. use

### 2.1. 扫描仓库

Scan a repo for only verified secrets

```
trufflehog git https://github.com/trufflesecurity/test_keys --results=verified,unknown
```

---

Refrences

- [trufflehog](https://github.com/trufflesecurity/trufflehog)