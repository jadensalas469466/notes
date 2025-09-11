Xray, Penetrates Everything. Also the best v2ray-core. Where the magic happens. An open platform for various uses.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ sudo bash -c "$(curl -fsSL https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install
```

## 2. Init

将 [v2ray-agent](https://github.com/mack-a/v2ray-agent) 生成的客户端配置文件写入 `config.json` 

```
┌──(nemo@debian)-[~]
└─$ sudo nano /usr/local/etc/xray/config.json && sudo systemctl restart xray
```

---

References

- [Xray-core](https://github.com/XTLS/Xray-core)

