## 1. 安装

```
curl -sSfL https://raw.githubusercontent.com/trufflesecurity/trufflehog/main/scripts/install.sh | sh -s -- -b /usr/local/bin
```

## 2. 使用

### 2.1. 扫描仓库

Scan a repo for only verified secrets

```
trufflehog git https://github.com/trufflesecurity/test_keys --results=verified,unknown
```