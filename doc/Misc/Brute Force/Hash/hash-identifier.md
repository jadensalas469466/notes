哈希值类型识别。

## 1 使用

运行

```shell
┌──(root㉿kali-23)-[~]
└─# hash-identifier
```

分析加密类型

```
 HASH: 10470c3b4b1fed12c3baac014be15fac67c6e815
```

```
Possible Hashs:
[+] SHA-1
[+] MySQL5 - SHA-1(SHA-1($pass))
```

> 加密类型可能为 SHA-1 或者 MySQL5 - SHA-1(SHA-1($pass))

---

References

- [hash-identifier](https://github.com/blackploit/hash-identifier)