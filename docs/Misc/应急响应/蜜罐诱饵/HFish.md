开源蜜罐。

## 1 环境搭建

Windows 节点的扫描感知依赖 WinPcap，需要手动进行下载安装

> https://www.winpcap.org/

> HFish 通过节点端构造“蜜罐服务”，因此，部署节点的机器不建议运行任何正常业务。
>
> 如果蜜罐节点上有正常业务致大量数据时候，可以通过扫描感知高级配置定向对节点或者端口开白名单

### 1.1 管理端

官网

>https://hfish.net/

防火墙开启4433、4434，确认返回success

```
[root@CentOS-76 ~]# firewall-cmd --add-port=4433/tcp --permanent
[root@CentOS-76 ~]# firewall-cmd --add-port=4434/tcp --permanent
[root@CentOS-76 ~]# firewall-cmd --reload
```

> 如果防火墙已禁用无需执行以上命令。
>
> 如之后蜜罐服务需要占用其他端口，可使用相同命令打开。

使用root用户，运行下面的脚本

```
[root@CentOS-76 ~]# bash <(curl -sS -L https://hfish.net/webinstall.sh)
```

安装

```
Input: 1
```

浏览器访问

> https://192.168.6.76:4433/web/

>默认账号：admin
>默认密码：HFish2021

查看节点和开启的蜜罐

![](./../../../../images/HFish/%E6%9F%A5%E7%9C%8B%E8%8A%82%E7%82%B9%E5%92%8C%E5%BC%80%E5%90%AF%E7%9A%84%E8%9C%9C%E7%BD%90.png)

> 有未启用的蜜罐是因为主机上启用了相应的服务，导致端口冲突

可更改默认端口

> 管理端不部署蜜罐的情况下不需要更改

```
[root@CentOS-76 ~]# vim /etc/ssh/sshd_config
```

```
#Port 22
Port 24
```

重启服务后生效

```
[root@CentOS-76 ~]# systemctl restart sshd.service
```

> 此时在 HFish 重启蜜罐即可

### 1.2 添加节点

**通过命令行单个安装节点**

配置节点架构和管理端地址

![](./../../../../images/HFish/%E9%85%8D%E7%BD%AE%E8%8A%82%E7%82%B9%E6%9E%B6%E6%9E%84%E5%92%8C%E7%AE%A1%E7%90%86%E7%AB%AF%E5%9C%B0%E5%9D%80.png)

**Linux**

复制命令行到目标执行

![](./../../../../images/HFish/%E5%A4%8D%E5%88%B6%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%88%B0%E7%9B%AE%E6%A0%87%E6%89%A7%E8%A1%8C.png)

**Windows**

下载程序到目标运行

![](./../../../../images/HFish/%E4%B8%8B%E8%BD%BD%E7%A8%8B%E5%BA%8F%E5%88%B0%E7%9B%AE%E6%A0%87%E8%BF%90%E8%A1%8C.png)

**通过 ssh 批量安装节点**

![](./../../../../images/HFish/%E9%80%9A%E8%BF%87%20ssh%20%E6%89%B9%E9%87%8F%E5%AE%89%E8%A3%85%E8%8A%82%E7%82%B9.png)

### 1.3 给节点添加蜜罐服务

将节点 client002 上 sshd 服务的 22 端口改为 24 端口。 

> 否则 ssh 蜜罐服务会占用 22 端口。

```
[root@CentOS-74 ~]# vim /etc/ssh/sshd_config
```

```
#Port 22
Port 24
```

重启 ssh 服务

```
[root@CentOS-74 ~]# systemctl restart sshd.service
```

**单独添加**

点击单个节点，可直接对节点上的服务进行添加和删除

![](./../../../../images/HFish/%E7%82%B9%E5%87%BB%E5%8D%95%E4%B8%AA%E8%8A%82%E7%82%B9%EF%BC%8C%E5%8F%AF%E7%9B%B4%E6%8E%A5%E5%AF%B9%E8%8A%82%E7%82%B9%E4%B8%8A%E7%9A%84%E6%9C%8D%E5%8A%A1%E8%BF%9B%E8%A1%8C%E6%B7%BB%E5%8A%A0%E5%92%8C%E5%88%A0%E9%99%A4.png)

添加以一下常用的蜜罐服务，然后点击确定

>高交互的 mysql 不能用

![](./../../../../images/HFish/%E6%B7%BB%E5%8A%A0%E4%BB%A5%E4%B8%80%E4%B8%8B%E5%B8%B8%E7%94%A8%E7%9A%84%E8%9C%9C%E7%BD%90%E6%9C%8D%E5%8A%A1%EF%BC%8C%E7%84%B6%E5%90%8E%E7%82%B9%E5%87%BB%E7%A1%AE%E5%AE%9A.png)

刷新浏览器

![](./../../../../images/HFish/%E5%88%B7%E6%96%B0%E6%B5%8F%E8%A7%88%E5%99%A8.png)

>“ssh 蜜罐” 和 “高交互 SSH 蜜罐” 不能同时使用，因为它们都使用 22 端口，会冲突。直接使用 “高交互 SSH 蜜罐” 即可。

**批量添加**

点击新增模板

![](./../../../../images/HFish/%E7%82%B9%E5%87%BB%E6%96%B0%E5%A2%9E%E6%A8%A1%E6%9D%BF.png)

填写模板名称，选择关联的蜜罐服务

![](./../../../../images/HFish/%E5%A1%AB%E5%86%99%E6%A8%A1%E6%9D%BF%E5%90%8D%E7%A7%B0%EF%BC%8C%E9%80%89%E6%8B%A9%E5%85%B3%E8%81%94%E7%9A%84%E8%9C%9C%E7%BD%90%E6%9C%8D%E5%8A%A1.png)

到节点管理，展开要添加蜜罐服务的节点

![](./../../../../images/HFish/%E5%88%B0%E8%8A%82%E7%82%B9%E7%AE%A1%E7%90%86%EF%BC%8C%E5%B1%95%E5%BC%80%E8%A6%81%E6%B7%BB%E5%8A%A0%E8%9C%9C%E7%BD%90%E6%9C%8D%E5%8A%A1%E7%9A%84%E8%8A%82%E7%82%B9.png)

选择模板，给节点增加蜜罐服务

![](./../../../../images/HFish/%E9%80%89%E6%8B%A9%E6%A8%A1%E6%9D%BF%EF%BC%8C%E7%BB%99%E8%8A%82%E7%82%B9%E5%A2%9E%E5%8A%A0%E8%9C%9C%E7%BD%90%E6%9C%8D%E5%8A%A1.png)

## 2 对蜜罐进行渗透

访问海康摄像头蜜罐

> http://192.168.6.74:9082

访问其它蜜罐服务

> http://192.168.6.74:9218

使用 nmap 扫描蜜罐 3306 端口（MySQL）

```
┌──(root㉿Kali-24)-[~]
└─# nmap 192.168.6.74 -p 3306
```

登录蜜罐 MySQL

```
┌──(root㉿Kali-24)-[~]
└─# mysql -u root -h 192.168.6.74
```

> 空密码直接登录

列出数据库

```
MySQL [(none)]> show databases;
```

退出

```
MySQL [(none)]> exit
```

>http://192.168.6.74:9197/	TP-LINK 路由器蜜罐
>
>http://192.168.6.74:9291/	Nginx 蜜罐
>
>http://192.168.6.74:9302/	北京疫情上报系统
>
>http://192.168.6.74:9303/	电站智慧监控运维管理云平台

北京疫情上报系统官网

> https://yqgz.beijing.gov.cn/service/logon

尝试登录高交互 ssh 服务

```
┌──(root㉿Kali-24)-[~]
└─# ssh -oHostKeyAlgorithms=+ssh-dss root@192.168.6.74
```

> 蜜罐的 ssh 服务版本较老，新版本直接 `ssh root@192.168.6.76` 即可
>
> 密码：123456

是一个假的 sshd 服务，尝试执行一些命令

```
[root@i-i57hue27 ~] pwd 
/root
[root@i-i57hue27 ~] echo 666 >hello.txt 
[root@i-i57hue27 ~] cat hello.txt 
666
```

## 3 查看数据

### 3.1 攻击列表

打开攻击列表

![](./../../../../images/HFish/%E6%89%93%E5%BC%80%E6%94%BB%E5%87%BB%E5%88%97%E8%A1%A8.png)

筛选节点

![](./../../../../images/HFish/%E7%AD%9B%E9%80%89%E8%8A%82%E7%82%B9.png)

查看详细信息

![](./../../../../images/HFish/%E6%9F%A5%E7%9C%8B%E8%AF%A6%E7%BB%86%E4%BF%A1%E6%81%AF.png)

可下载攻击者写入的文件

![](./../../../../images/HFish/%E5%8F%AF%E4%B8%8B%E8%BD%BD%E6%94%BB%E5%87%BB%E8%80%85%E5%86%99%E5%85%A5%E7%9A%84%E6%96%87%E4%BB%B6.png)

下载数据

![](./../../../../images/HFish/%E4%B8%8B%E8%BD%BD%E6%95%B0%E6%8D%AE.png)

对攻击来源操作

![](./../../../../images/HFish/%E5%AF%B9%E6%94%BB%E5%87%BB%E6%9D%A5%E6%BA%90%E6%93%8D%E4%BD%9C.png)

>标记
>
>搜索
>
>忽略
>
>复制
>
>添加白名单
>
>查看 IP 画像

查看 IP 画像可得到 设备信息，如 UA

### 3.2 基于 IP 进行定位

查询 IP `92.255.85.115`

浏览器访问，查看城市

> https://ip138.com/

开启 Best Trace路由跟踪

![](./../../../../images/HFish/%E5%BC%80%E5%90%AF%20Best%20Trace%E8%B7%AF%E7%94%B1%E8%B7%9F%E8%B8%AA.png)

输入 IP 定位

![](./../../../../images/HFish/%E8%BE%93%E5%85%A5%20IP%20%E5%AE%9A%E4%BD%8D.png)

国内的 IP 地址，可以基于 IP 地址准确定位

> https://www.ipip.net/ipquery.html

目标 IP `111.192.146.73`

> 经纬度：`116.126854,40.071533`

得到经纬度，可通过坐标反查

>http://api.map.baidu.com/lbsapi/getpoint/index.html
>
>经纬度： `116.126854,40.071533`
>
>https://www.google.de/maps/
>
>纬经度： `40.071533,116.126854`

![](./../../../../images/HFish/%E5%BE%97%E5%88%B0%E7%BB%8F%E7%BA%AC%E5%BA%A6%EF%BC%8C%E5%8F%AF%E9%80%9A%E8%BF%87%E5%9D%90%E6%A0%87%E5%8F%8D%E6%9F%A5.png)

### 3.3  扫描感知

收集节点机器网卡的所有连接信息

>展示 HFish 蜜罐节点被 TCP、UDP 和 ICMP 三种协议的全端口扫描探测行为

![](./../../../../images/HFish/%E6%94%B6%E9%9B%86%E8%8A%82%E7%82%B9%E6%9C%BA%E5%99%A8%E7%BD%91%E5%8D%A1%E7%9A%84%E6%89%80%E6%9C%89%E8%BF%9E%E6%8E%A5%E4%BF%A1%E6%81%AF.png)

>即使节点相关端口没有开放，HFish 仍能记录下扫描行为，此外，HFish 还会记录节点主机本身外联行为

### 3.4 攻击来源

收集了所有连接和攻击节点的 IP 信息

>所有尝试连接和攻击节点的 IP 信息都被记录在攻击来源中，如果蜜罐溯源和反制成功，信息也会被记录其中。

![](./../../../../images/HFish/%E6%94%B6%E9%9B%86%E4%BA%86%E6%89%80%E6%9C%89%E8%BF%9E%E6%8E%A5%E5%92%8C%E6%94%BB%E5%87%BB%E8%8A%82%E7%82%B9%E7%9A%84%20IP%20%E4%BF%A1%E6%81%AF.png)

### 3.5 账号资源

收集了所有攻击者破解蜜罐使用的账号密码

>HFish 会提取攻击者对 SSH、以及所有 Web 蜜罐登录所使用的账号密码，进行统一展示。同时，用户可自定义监控词汇，如员工姓名、公司名称等，一旦与攻击者使用的账号重合，可高亮显示并告警
>
>该页面用于收集所有被用来攻击的账号密码，通过配置可对企业失陷账号进行有效监控

设定高级监测策略，监控泄漏

![](./../../../../images/HFish/%E8%AE%BE%E5%AE%9A%E9%AB%98%E7%BA%A7%E7%9B%91%E6%B5%8B%E7%AD%96%E7%95%A5%EF%BC%8C%E7%9B%91%E6%8E%A7%E6%B3%84%E6%BC%8F.png)

> 可查看到所有匹配高级监测策略的数据，帮助安全人员精准排查泄漏账号。

>最后，如果有用户因为外网 ip 测试，导致 ip 被给了恶意标签的话，可以邮件
>Honeypot@threatbook.cn 说明情况。

## 4 溯源

溯源，一般是在攻防中，用于挖掘攻击者身份，通过资产面，回溯等判断攻击者身份。在近几年攻防演练中，更加特指了解对方的身份信息。



HFish 共支持三种溯源手段

> Mysql 反制（支持内网，能够对攻击者机器做任意文件读取）
>
> 厂商 vpn 蜜罐反制（支持内网，能够获得 windows 机器登录的微信号信息与桌面截图）
>
> web 型蜜罐溯源（不支持内网）这种溯源方式，在溯源时，会自动获取攻击者的出口 IP 进行标记

### 4.1 溯源实现

**MySQL 反制**

支持内网，能够对攻击者机器做任意文件读取

>通过 MySQL 客户端漏洞，当攻击者使用 8.0 以下的 Mysql 客户端直连 HFish 的 MySQL 蜜罐的时候。可以触发任意文件读取的能力，读取 MySQL 客户端所在机器上的任意一个文件。

>注意：
>一定是 MySQL 客户端直连。不兼容诸如 navicat 这类工具。
>在节点管理中，可以设置 mysql 任意文件读取的具体读取路径。
>这里设置内置节点的 MySQL 蜜罐

配置 MySQL 反制

![](./../../../../images/HFish/%E9%85%8D%E7%BD%AE%20MySQL%20%E5%8F%8D%E5%88%B6.png)

写入需要从攻击者读取的文件

![](./../../../../images/HFish/%E5%86%99%E5%85%A5%E9%9C%80%E8%A6%81%E4%BB%8E%E6%94%BB%E5%87%BB%E8%80%85%E8%AF%BB%E5%8F%96%E7%9A%84%E6%96%87%E4%BB%B6.png)

**厂商 vpn 蜜罐反制**

支持内网，能够获得 windows 机器登录的微信号信息与桌面截图

>通过蜜罐页面提供可下载二进制，攻击者下载执行后，会获取攻击者的微信与屏幕截图。

Windows 浏览器访问

> http://192.168.6.74:9091/

点击 Download Client 下载 VPN 客户端

运行 EasyConnectInstaller.exe

打开攻击来源，找到攻击 IP 为 Windows10 的 192.168.6.102 的记录

下载微信溯源信息

![](./../../../../images/HFish/%E4%B8%8B%E8%BD%BD%E5%BE%AE%E4%BF%A1%E6%BA%AF%E6%BA%90%E4%BF%A1%E6%81%AF.png)

> 可查看攻击者桌面截图

**Web 型蜜罐溯源**

不支持内网溯源

> HFish 所有的 web 页面蜜罐，包括自定义蜜罐，都可以在该情况下进行溯源
>
> 对扫描器、webshell 管理器、java 反序列化反制。该部分反制数据会显示攻击者的出口 IP。
>
> 可以拿到包括机器架构，微信账号、QQ 账号、QQ 音乐账号、百度云账号，浏览器浏览记录、history、whoami 等信息。
>
> 注意：这部分只支持企业安全部门的测试申请与协助。

需要向 HFish 官方申请

### 4.2 威胁检测

根据需求手动创建威胁检测规则

>本地默认自带规则，通过设置自定义规则，可对关注的重点攻击行为做实时监控。
>
>在重大保障/攻防演练中，当有 0day、Nday 等漏洞爆出，可自定义添加对应漏洞的 yara 规则，重点监控。
>
>另外，威胁检测引擎会发现触发这些规则的告警，这些告警可帮助判断针对性攻击。

>HFish 的威胁检测引擎是基于攻击 HFish 的日志数据进行检测。
>
>日志原始数据可以查看攻击列表。
>
>这些数据包括有 web 蜜罐的 url 数据、UA 等数据，高交互蜜罐内执行的命令等数据，普通蜜罐的记录日志。

![](./../../../../images/HFish/%E6%A0%B9%E6%8D%AE%E9%9C%80%E6%B1%82%E6%89%8B%E5%8A%A8%E5%88%9B%E5%BB%BA%E5%A8%81%E8%83%81%E6%A3%80%E6%B5%8B%E8%A7%84%E5%88%99.png)

> 可在攻击列表获取原始数据
>
> 通过增加威胁检测引擎，支持规则检测，且支持上传自定义 yara 规则，系统自动化分析数据，判定攻击行为，丰富 IP 威胁判定，更清晰的感受攻击态势和攻击情况。

### 4.2.1 HFish 检测语法

HFish 使用的 yara 规则检测语法分为三部分，`rule`，`string` 和 `condition`

样例：

```
rule name1
{
strings:
$str1 = "1"
$str2 = "2"

condition:
any of them
}
```

>该样例代表的是，建立了一个叫做 "name1" 的检测规则，如果检测的数据中出现 1 或者 2，代表这个数据触碰了我建立的 name1 规则。

Yara 检测规则语法参考

> https://yara.readthedocs.io/en/v4.1.2/index.html

规则名称: MySQL 数据库被连接

```
rule MySQL_login_check
{
strings:
$str1 = "already connected" nocase
$str2 = "show databases" nocase

condition:
any of them
}
```

>说明：建立了一个叫做 " MySQL_login_check " 的检测规则，如果检测的数据中出现 "already connected" 或者 "show databases"，就会触碰这个规则，yara 中默认文本字符串是区分大小写的，但是可以通过在字符串定义的末尾附加修饰符 nocase 将字符串转换为不区分大小写的模式。

## 5 失陷感知

蜜饵

HFish 的蜜饵在牵引攻击者的功能上增加了精确定位失陷能力，即每个蜜饵都是唯一的，攻击者入侵用户主机后，如果盗取蜜饵文件中的数据并从任意主机发起攻击，防守者仍能知道失陷源头在哪里。

>由于蜜饵只是静态文件，所以蜜饵适合部署在任何主机和场景中，例如作为附件通过邮件发送（检测邮件是否被盗）、在攻防演练期间上传到百度网盘或 github 上混淆攻击者视线、压缩改名成 backup.zip 放置在 Web 目录下守株待兔等待攻击者扫描器上钩。

蜜标

>HFish 的蜜标为 excel 或者 word 文件的格式，一个蜜标可以下发到多个主机。攻击者入侵用户主机后，只要尝试打开蜜标，那么蜜标就会给节点发出告警信息。我们最终可以在管理端看到整体的蜜标失陷告警。
>
>因此特别注意：蜜标在多个机器部署的时候，蜜标部署位置一定要跟生成蜜标的节点是可联通的。

密饵和密标的区别

>文件蜜饵：文件蜜饵被下载到布防机器后，如果攻击者打开该文件，并按照指令操作，HFish 将感知威胁，并告警。文件格式为 .txt 或 .cfg 等。
>
>文件蜜标：文件蜜标被下载到布防机器后，如果攻击者打开该文件，HFish 将感知威胁，并告警。文件格式为 word 或 excel 等。
>
>HFish 的诱饵模块由定制、分发接口和告警信息三部分组成。

### 5.1 诱饵定制

新增诱饵

![](./../../../../images/HFish/%E6%96%B0%E5%A2%9E%E8%AF%B1%E9%A5%B5.png)

这里选择文件蜜饵

![](./../../../../images/HFish/%E8%BF%99%E9%87%8C%E9%80%89%E6%8B%A9%E6%96%87%E4%BB%B6%E8%9C%9C%E9%A5%B5.png)

配置蜜饵

![](./../../../../images/HFish/%E9%85%8D%E7%BD%AE%E8%9C%9C%E9%A5%B5.png)

> 在蜜饵内容中， `$username$` 、 `$password$` 和 `$honeypot$` 分别代表账号、密码和蜜罐变量，以上为必填变量，必须进行引用，才能让蜜饵功能生效。 三个变量按照文件想呈现给攻击者的效果进行引用

| 操作       | 描述                                                       |
| ---------- | ---------------------------------------------------------- |
| $username$ | 变量如果未填写账号字典，则默认用 root 作为所有蜜饵的账号名 |
| $password$ | 变量按照选取的位数，自动生成蜜饵的密码                     |
| $honeypot$ | 变量按照蜜饵下拉节点的部署服务，自动生成 IP 和端口         |

>蜜饵名称：	`Linux 系统远程登录帐号汇总` 或 `account_info`
>蜜饵描述：	`此文件存储公司 Linux 服务器的用户和密码`

点查看示例 

![](./../../../../images/HFish/%E7%82%B9%E6%9F%A5%E7%9C%8B%E7%A4%BA%E4%BE%8B%20.png)

复制内容

![](./../../../../images/HFish/%E5%A4%8D%E5%88%B6%E5%86%85%E5%AE%B9.png)

```
$honeypot$
$username$
$password$
ndq_limit=500
ndq_spoof=/mnt/
```

输入后点击预览

![](./../../../../images/HFish/%E8%BE%93%E5%85%A5%E5%90%8E%E7%82%B9%E5%87%BB%E9%A2%84%E8%A7%88.png)

点击确定，即可新增一条文件蜜饵

### 5.2 密饵分发

在节点管理选择节点

![](./../../../../images/HFish/%E5%9C%A8%E8%8A%82%E7%82%B9%E7%AE%A1%E7%90%86%E9%80%89%E6%8B%A9%E8%8A%82%E7%82%B9.png)

开启失陷蜜饵状态

![](./../../../../images/HFish/%E5%BC%80%E5%90%AF%E5%A4%B1%E9%99%B7%E8%9C%9C%E9%A5%B5%E7%8A%B6%E6%80%81.png)

部署蜜饵

![](./../../../../images/HFish/%E9%83%A8%E7%BD%B2%E8%9C%9C%E9%A5%B5.png)

复制命令到节点上执行

```
[root@CentOS-74 ~]# curl -o /tmp/account_info.cfg http://192.168.6.74:7878/download/bait/5
```

> 蜜饵已部署到 /tmp 目录下

部署完成后在失陷感知查看

![](./../../../../images/HFish/%E9%83%A8%E7%BD%B2%E5%AE%8C%E6%88%90%E5%90%8E%E5%9C%A8%E5%A4%B1%E9%99%B7%E6%84%9F%E7%9F%A5%E6%9F%A5%E7%9C%8B.png)

> 如果攻击者根据已部署的蜜饵文件中的虚假信息尝试登录，HFish 将会记录并告警，并展示已失陷节点主机和失陷流程。

### 5.3 触发密饵

使用 xshell 连接到节点，模拟攻击者下载蜜饵文件

```
[root@CentOS-74 ~]# sz /tmp/account_info.cfg
```

访问该文件

```
#登陆方式：
ip=192.168.6.74
port=9224
protocol=http
username=admin
password=B1YezlwC
ndq_limit=500
ndq_spoof=/mnt/
```

按照文件中写的方式尝试去登录

>http://192.168.6.74:9224/
>
>账号	admin
>密码	B1YezlwC

到失陷感知中查看诱饵的失陷状态

> 已失陷

## 6 样本检测

该页面用于展示 HFish 在高交互蜜罐（高交互 ssh 和高交互 telnet 蜜罐）中，捕获到的攻击者上传下载到服务器中的样本。
所有样本都会上传到免费的微步在线沙箱（https://s.threatbook.cn/)中，进行样本检测，并将结果返回。该检测不花费用户检测次数。

>此实验建议使用云服务器搭建蜜罐去做，因为 HFish 高交互蜜罐部署在云服务器，由 HFish 团队做统一运维。攻击者与用户本地发生的流量交互都会被转发到云端蜜网，所有的威胁行为都在云端蜜网发生

云端高交互蜜罐默认配置在服务管理中

>节点可联通 zoo.hfish.net
>管理端可联通 zoo.hfish.net、api.hfish.net
>确认网络联通后，直接在节点中添加高交互蜜罐服务即可。

开启高交互 SSH 服务，连接

```
账号	root
密码	123456
```

```
[root@CentOS-76 ~]# ssh root@192.168.6.74
[root@i-i57hue27 ~] 
```

模拟下载后门程序

```
[root@i-i57hue27 ~] wget http://issuecdn.baidupcs.com/issue/netdisk/yunguanjia/BaiduNetdisk_5.5.3.exe
```

>攻击者登录进高交互 SSH 蜜罐，上传或下载到服务器的文件都会上传到免费的微步在线沙箱（https://s.threatbook.cn/)中，进行样本检测，并将结果返回

查看样本检测

![](./../../../../images/HFish/%E6%9F%A5%E7%9C%8B%E6%A0%B7%E6%9C%AC%E6%A3%80%E6%B5%8B.png)

查看详情

![](./../../../../images/HFish/%E6%9F%A5%E7%9C%8B%E8%AF%A6%E6%83%85.png)

## 7 卸载 HFish 蜜罐

> https://hfish.net/

### 7.1 卸载管理端

删除计划任务进程

```
[root@CentOS-76 ~]# crontab -e
```

```
* * * * * /opt/hfish/hfish
```

> 删除以上内容

结束管理端进程

```
[root@CentOS-76 ~]# ps ax | grep ./hfish | grep -v grep
  3996 ?        Ssl    0:29 /opt/hfish/hfish
  4010 ?        Ssl    1:24 /opt/hfish/hfish-server -d /opt/hfish/3.3.1
[root@CentOS-76 ~]# kill -9 3996
[root@CentOS-76 ~]# kill -9 4010
```

删除文件夹

```
[root@CentOS-76 ~]# rm -rf /opt/hfish
```

清理所有配置

> 如果后续还要安装，建议不要删除，否则下次使用需要完全重新配置

```
[root@CentOS-76 ~]# rm -rf /usr/share/hfish
```

删除HFish数据库

```
[root@CentOS-76 ~]# mysql -h127.0.0.1 -uroot -p
```

停止MySQL服务

```
[root@CentOS-76 ~]# systemctl stop mysqld.service
[root@CentOS-76 ~]# systemctl disable mysqld.service
```

清除 SSH config 内对于访问来源的限制（根据需要设置）

```
[root@CentOS-76 ~]# vim /etc/ssh/sshd_config
```

> 注释掉以 AllowUsers root@ 开头的行

重启SSH服务

```
[root@CentOS-76 ~]# systemctl restart sshd.service
```

清除 Firewall 服务的规则（请根据实际情况删除！）

```
[root@CentOS-76 ~]# firewall-cmd --permanent --list-all | grep ports | head -n 1 | \
cut -d: -f2 | tr ' ' '\n' | xargs -I {} firewall-cmd --permanent --remove-port={}
```

重启Firewall服务

```
[root@CentOS-76 ~]# systemctl restart firewalld.service
```

### 7.2 卸载节点端

删除计划任务进程

```
[root@CentOS-74 ~]# crontab -e
```

```
* * * * * /root/hfishclient/client
```

> 删除以上内容

结束client进程

```
[root@CentOS-74 ~]# ps ax | grep ./client | grep -v grep
[root@CentOS-74 ~]# kill -9 2985
```

删除client文件夹

```
[root@CentOS-74 ~]# rm -rf hfishclient/
```

---

参考链接

- [HFish](https://hfish.net/)
