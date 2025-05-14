综合信息收集工具。

## 1 安装

安装

```shell
┌──(root㉿kali)-[~]
└─# sudo apt install -y gobuster
```

## 2 使用

调用字典对目标进行目录扫描

```shell
┌──(root㉿kali)-[~]
└─# gobuster dir -u [url] -w /usr/share/wordlists/dirb/common.txt
```

---

Refrences

- [Gobuster](https://www.kali.org/tools/gobuster/)
