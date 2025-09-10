综合靶场.

## 1. Install

克隆仓库

```
git clone --depth 1 https://github.com/vulhub/vulhub.git
```

## 2. Usage

查看漏洞环境

```
ls ~/vulhub
```

启动漏洞环境

```
cd ~/vulhub/path \
&& docker compose build \
&& docker compose up -d
```

查看文档

```
┌──(sec@debian)-[~/vulhub/path]
└─# less README.zh-cn.md
```

删除环境

```
┌──(sec@debian)-[~/vulhub/path]
└─# docker compose down -v
```

---

References

- [Vulhub](https://vulhub.org/)

