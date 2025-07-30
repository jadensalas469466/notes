一款网站管理工具。

## 1 安装

下载加载器

```shell
┌──(root㉿kali-23)-[~]
└─# proxychains4 curl -LO 'https://github.com/AntSwordProject/AntSword-Loader/releases/download/4.0.3/AntSword-Loader-v4.0.3-linux-x64.zip'  && unzip /root/AntSword-Loader-v4.0.3-linux-x64.zip -d /root/tools && rm -rf /root/AntSword-Loader-v4.0.3-linux-x64.zip
```

下载源代码

```shell
┌──(root㉿kali-23)-[~]
└─# cd /root/tools/AntSword-Loader-v4.0.3-linux-x64 && git clone https://github.com/AntSwordProject/antSword.git --depth=1
```

运行加载器后初始化加载源代码

```shell
┌──(root㉿kali-23)-[~/tools/AntSword-Loader-v4.0.3-linux-x64]
└─# ./AntSword
```

![运行加载器后初始化加载源代码](./../../../images/AntSword/%E8%BF%90%E8%A1%8C%E5%8A%A0%E8%BD%BD%E5%99%A8%E5%90%8E%E5%88%9D%E5%A7%8B%E5%8C%96%E5%8A%A0%E8%BD%BD%E6%BA%90%E4%BB%A3%E7%A0%81.png)

编写脚本

```shell
┌──(root㉿kali-23)-[~/tools/AntSword-Loader-v4.0.3-linux-x64]
└─# vim antsword.sh
```

```shell
#!/bin/bash

# 获取链接的实际路径并切换到该目录
cd "$(dirname "$(readlink -f "$0")")"

# 运行 antsword
./AntSword "$@"

```

创建链接

```shell
┌──(root㉿kali-23)-[~/tools/AntSword-Loader-v4.0.3-linux-x64]
└─# chmod +x antsword.sh && ln -s /root/tools/AntSword-Loader-v4.0.3-linux-x64/antsword.sh /usr/local/bin/antsword
```

## 2 使用

右键选择添加数据

![](./../../../images/AntSword/%E5%8F%B3%E9%94%AE%E9%80%89%E6%8B%A9%E6%B7%BB%E5%8A%A0%E6%95%B0%E6%8D%AE.png)

填写基础配置

```
http://192.168.6.76/upload/webshell.php
```

![](./../../../images/AntSword/%E5%A1%AB%E5%86%99%E5%9F%BA%E7%A1%80%E9%85%8D%E7%BD%AE.png)

填写请求信息，防止被入侵

![](./../../../images/AntSword/%E5%A1%AB%E5%86%99%E8%AF%B7%E6%B1%82%E4%BF%A1%E6%81%AF%EF%BC%8C%E9%98%B2%E6%AD%A2%E8%A2%AB%E5%85%A5%E4%BE%B5.png)

### 2.1 操作

双击进入目标 Web 目录

![](./../../../images/AntSword/%E5%8F%8C%E5%87%BB%E8%BF%9B%E5%85%A5%E7%9B%AE%E6%A0%87%20Web%20%E7%9B%AE%E5%BD%95%20(1).png)

![](./../../../images/AntSword/%E5%8F%8C%E5%87%BB%E8%BF%9B%E5%85%A5%E7%9B%AE%E6%A0%87%20Web%20%E7%9B%AE%E5%BD%95%20(2).png)

可下载根目录下的所有文件

![](./../../../images/AntSword/%E5%8F%AF%E4%B8%8B%E8%BD%BD%E6%A0%B9%E7%9B%AE%E5%BD%95%E4%B8%8B%E7%9A%84%E6%89%80%E6%9C%89%E6%96%87%E4%BB%B6.png)

也可直接修改文件

![](./../../../images/AntSword/%E4%B9%9F%E5%8F%AF%E7%9B%B4%E6%8E%A5%E4%BF%AE%E6%94%B9%E6%96%87%E4%BB%B6%20(1).png)

![也可直接修改文件 (2)](./../../../images/AntSword/%E4%B9%9F%E5%8F%AF%E7%9B%B4%E6%8E%A5%E4%BF%AE%E6%94%B9%E6%96%87%E4%BB%B6%20(2).png)

新建文件（只能在有 apache 权限的目录下创建）

![](./../../../images/AntSword/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%20(1).png)

![新建文件 (2)](./../../../images/AntSword/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%20(2).png)

浏览器访问写入的文件

![](./../../../images/AntSword/%E6%B5%8F%E8%A7%88%E5%99%A8%E8%AE%BF%E9%97%AE%E5%86%99%E5%85%A5%E7%9A%84%E6%96%87%E4%BB%B6.png)

> 可上传木马文件

右键打开终端

![](./../../../images/AntSword/%E5%8F%B3%E9%94%AE%E6%89%93%E5%BC%80%E7%BB%88%E7%AB%AF.png)

进入设置更改字体大小

![](./../../../images/AntSword/%E8%BF%9B%E5%85%A5%E8%AE%BE%E7%BD%AE%E6%9B%B4%E6%94%B9%E5%AD%97%E4%BD%93%E5%A4%A7%E5%B0%8F%20(1).png)

![](./../../../images/AntSword/%E8%BF%9B%E5%85%A5%E8%AE%BE%E7%BD%AE%E6%9B%B4%E6%94%B9%E5%AD%97%E4%BD%93%E5%A4%A7%E5%B0%8F%20(2).png)

可在此终端执行命令

![](./../../../images/AntSword/%E5%8F%AF%E5%9C%A8%E6%AD%A4%E7%BB%88%E7%AB%AF%E6%89%A7%E8%A1%8C%E5%91%BD%E4%BB%A4.png)

使用 BurpSuite 对蚁剑连接一句话木马抓包，分析虚拟终端原理

> [BurpSuite.md](..\..\03-Web程序\BurpSuite\BurpSuite.md) 

### 2.1.1 上传大马

直接将大马拖拽到站点目录

![直接将大马拖拽到站点目录](./../../../images/AntSword/%E7%9B%B4%E6%8E%A5%E5%B0%86%E5%A4%A7%E9%A9%AC%E6%8B%96%E6%8B%BD%E5%88%B0%E7%AB%99%E7%82%B9%E7%9B%AE%E5%BD%95.png)

访问即可

>http://purple.local/test.php
>
>密码：hacker

---

References

- [AntSword 加载器](https://github.com/AntSwordProject/AntSword-Loader)
- [AntSword](https://github.com/AntSwordProject/antSword)