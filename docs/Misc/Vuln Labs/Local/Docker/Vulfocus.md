## 1. Install

Run

```
┌──(nemo@debian)-[~]
└─$ docker run -d --restart always -p 60088:80 -v /var/run/docker.sock:/var/run/docker.sock -e VUL_IP=127.0.0.1 Vulfocus/Vulfocus
```

## 2. Init

Port Forwarding Rules

| Name     | Host Port | Guest Port |
| -------- | --------- | ---------- |
| Vulfocus | 60088     | 60088      |

Visit

> http://127.0.0.1:60088

Login

```
admin:admin
```

修改系统配置

![修改系统配置](./../../../../../images/Vulfocus/%E4%BF%AE%E6%94%B9%E7%B3%BB%E7%BB%9F%E9%85%8D%E7%BD%AE.png)

|                          Vulfocus                           |
| :---------------------------------------------------------: |
| [pikachu](https://github.com/zhuifengshaonianhanlu/pikachu) |
|       [xss-labs](https://github.com/do0dl3/xss-labs)        |
|      [sqli-labs](https://github.com/Audi-1/sqli-labs)       |
|     [upload-labs](https://github.com/c0ny1/upload-labs)     |

## 3. Usage

同步镜像, 下载靶场
![同步镜像, 下载靶场](./../../../../../images/Vulfocus/%E5%90%8C%E6%AD%A5%E9%95%9C%E5%83%8F,%20%E4%B8%8B%E8%BD%BD%E9%9D%B6%E5%9C%BA.png)

启动靶场

![启动靶场](./../../../../../images/Vulfocus/%E5%90%AF%E5%8A%A8%E9%9D%B6%E5%9C%BA.png)

镜像信息

![镜像信息](./../../../../../images/Vulfocus/%E9%95%9C%E5%83%8F%E4%BF%A1%E6%81%AF.png)

Port Forwarding Rules

| Name    | Host Port | Guest Port |
| ------- | --------- | ---------- |
| example | port      | port       |

Visit

> http://127.0.0.1:port

手动停止

![手动停止](./../../../../../images/Vulfocus/%E6%89%8B%E5%8A%A8%E5%81%9C%E6%AD%A2.png)

---

References

- [Vulfocus](https://fofapro.github.io/Vulfocus/#/)

