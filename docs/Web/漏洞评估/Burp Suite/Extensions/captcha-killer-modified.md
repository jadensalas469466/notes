一款用于验证码爆破的 Burp Suite 插件。

## 1 安装

安装依赖

```powershell
PS D:\share> pip install argparse ddddocr
```

运行 [codereg](https://github.com/f0ng/captcha-killer-modified/blob/main/codereg.py) 

```
欢迎使用ddddocr，本项目专注带动行业内卷，个人博客:wenanzhe.com
训练数据支持来源于:http://146.56.204.113:19199/preview
爬虫框架feapder可快速一键接入，快速开启爬虫之旅：https://github.com/Boris-code/feapder
谷歌reCaptcha验证码 / hCaptcha验证码 / funCaptcha验证码商业级识别接口：https://yescaptcha.com/i/NSwk7i
======== Running on http://0.0.0.0:8888 ========
(Press CTRL+C to quit)
```

## 2 使用

点击刷新验证码，将请求数据包发送到 captcha-killer-modified

![点击刷新验证码，将请求数据包发送到 captcha-killer-modified](./../../../../../images/captcha-killer-modified/%E7%82%B9%E5%87%BB%E5%88%B7%E6%96%B0%E9%AA%8C%E8%AF%81%E7%A0%81%EF%BC%8C%E5%B0%86%E8%AF%B7%E6%B1%82%E6%95%B0%E6%8D%AE%E5%8C%85%E5%8F%91%E9%80%81%E5%88%B0%20captcha-killer-modified.png)

获取验证码

![获取验证码](./../../../../../images/captcha-killer-modified/%E8%8E%B7%E5%8F%96%E9%AA%8C%E8%AF%81%E7%A0%81.png)

从模板库创建 ddddocr

![从模板库创建 ddddocr](./../../../../../images/captcha-killer-modified/%E4%BB%8E%E6%A8%A1%E6%9D%BF%E5%BA%93%E5%88%9B%E5%BB%BA%20ddddocr.png)

识别验证码

![识别验证码](./../../../../../images/captcha-killer-modified/%E8%AF%86%E5%88%AB%E9%AA%8C%E8%AF%81%E7%A0%81.png)

开启使用插件，保证验证码自动识别

![开启使用插件，保证验证码自动识别](./../../../../../images/captcha-killer-modified/%E5%BC%80%E5%90%AF%E4%BD%BF%E7%94%A8%E6%8F%92%E4%BB%B6%EF%BC%8C%E4%BF%9D%E8%AF%81%E9%AA%8C%E8%AF%81%E7%A0%81%E8%87%AA%E5%8A%A8%E8%AF%86%E5%88%AB.png)

在 Intruder 中使用需要选择 Pitchfork 模式

![在 Intruder 中使用需要选择 Pitchfork 模式](./../../../../../images/captcha-killer-modified/%E5%9C%A8%20Intruder%20%E4%B8%AD%E4%BD%BF%E7%94%A8%E9%9C%80%E8%A6%81%E9%80%89%E6%8B%A9%20Pitchfork%20%E6%A8%A1%E5%BC%8F.png)

Payload 2 要选择 captcha-killer-modified

![Payload 2 要选择 captcha-killer-modified](./../../../../../images/captcha-killer-modified/Payload%202%20%E8%A6%81%E9%80%89%E6%8B%A9%20captcha-killer-modified.png)

资源池限制并发请求数和请求间隔

> 否则 ocr 无法及时识别

![资源池限制并发请求数和请求间隔](./../../../../../images/captcha-killer-modified/%E8%B5%84%E6%BA%90%E6%B1%A0%E9%99%90%E5%88%B6%E5%B9%B6%E5%8F%91%E8%AF%B7%E6%B1%82%E6%95%B0%E5%92%8C%E8%AF%B7%E6%B1%82%E9%97%B4%E9%9A%94.png)

---

参考链接

- [captcha-killer-modified](https://github.com/f0ng/captcha-killer-modified)
