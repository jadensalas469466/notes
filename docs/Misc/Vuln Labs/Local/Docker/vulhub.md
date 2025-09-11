综合靶场.

## 1. Install

克隆仓库到

```
┌──(sec@debian)-[~]
└─$ git clone --depth 1 https://github.com/vulhub/vulhub.git ~/.local/vulhub
```

## 2. Usage

查看漏洞环境

```
┌──(sec@debian)-[~]
└─$ ls  ~/.local/vulhub
```

启动漏洞环境

```
┌──(sec@debian)-[~]
└─$ cd ~/.local/vulhub/nday \
&& docker compose build \
&& docker compose up -d
```

查看文档

```
┌──(nemo@infosec)-[~/.local/vulhub/nday]
└─$ less README.zh-cn.md
```

删除环境

```
┌──(sec@debian)-[~/.local/vulhub/nday]
└─# docker compose down -v
```

---

References

- [Vulhub](https://vulhub.org/)

