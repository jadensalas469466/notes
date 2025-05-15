TruffleHog is the most powerful secrets Discovery, Classification, Validation, and Analysis tool. In this context secret refers to a credential a machine uses to authenticate itself to another machine. This includes API keys, database passwords, private encryption keys, and more...

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

- [truffleHog](https://www.kali.org/tools/trufflehog/)