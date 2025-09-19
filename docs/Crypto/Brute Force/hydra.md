Hydra is a parallelized login cracker which supports numerous protocols to attack. It is very fast and flexible, and new modules are easy to add.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y hydra
```

## 2. Usage

basic auth

```
┌──(nemo@debian)-[~]
└─$ hydra <host> -s <port> http-get /[protected_page] -L username.txt -P password.txt -e ns -vV
```

ssh

```
┌──(nemo@debian)-[~]
└─$ hydra <host> ssh -l root -P password.txt -t 4 -e ns -vV
```

ftp

```
┌──(nemo@debian)-[~]
└─$ hydra <host> ftp -L username.txt -P password.txt -e ns -vV
```

---

References

- [hydra](https://www.kali.org/tools/hydra/)
