搭建高匿代理

![搭建高匿代理](./../../../../../../image/v2ray-agent/%E6%90%AD%E5%BB%BA%E9%AB%98%E5%8C%BF%E4%BB%A3%E7%90%86.svg)

1. VLESS 建立服务端和客户端的通信.
2. Reality 伪装 VLESS 流量, 使其看起来像是常见的 HTTPS 流量.
3. uTLS 隐藏 TLS 特征.
4. Vision 对流量进行混淆.
5. Web 服务器转发流量.
6. 代理服务访问真正的目标网站.

配置代理

```
┌──(sec@debian)-[~]
└─# curl -LO https://github.com/mack-a/v2ray-agent/raw/master/install.sh \
&& su -c "bash ./install.sh && rm -f ./install.sh && exit"
```

```
请选择:2.任意组合安装
请选择:1.Xray-core
请选择:7.VLESS+Reality+uTLS+Vision[推荐]
```

> 仅保留二维码 VLESS(VLESS+reality+uTLS+Vision) 即可
>
> 记得使用 `sudo ufw allow <port>` 开放端口

---

References

- [v2ray-agent](https://github.com/mack-a/v2ray-agent)

