快速侦察与目标关联的互联网资产.

## 1 部署

[配置 Docker 容器引擎](https://keithpeck177271.gitbook.io/notes/misc/shi-yan-huan-jing/rong-qi/yin-qing/docker)

配置安全组开放 5003 端口

下载安装脚本

```shell
┌──(root㉿kali)-[~]
└─# wget https://raw.githubusercontent.com/Aabyss-Team/ARL/master/misc/setup-arl.sh
```

为安装脚本添加执行权限并运行

```shell
┌──(root㉿kali)-[~]
└─# chmod +x ./setup-arl.sh && ./setup-arl.sh && rm -rf ./setup-arl.sh
```

```
第一次安装建议进行换源参数在继续安装
1) 换源 (脚本来自于 https://github.com/SuperManito/LinuxMirrors)
2) 源码安装(暂时只支持centos 7 8 and Ubuntu20.04 支持国内外 安装)
3) docker安装 （支持国内外安装，但可能存在抽风问题）
4) 卸载Docker镜像
5) 添加指纹（默认为7k+）只限于源码安装添加指纹
6) 退出脚本
---------------------------------------------------------------
输入对应数字:3
```

```
Docker安装
安装环境确认 [国外环境输1  国内环境输2] > 2
```

```
请选择要安装的版本：
1) arl-docker-all：honmashironeko docker(暂时支持国外安装)
请输入选项（1）：1
```

```
请选择是否需要更换 yum 或 apt 下载源：
1) 不进行更换，使用默认下载源
2) 运行替换脚本，更换下载源
请输入选项（1-2）[默认1]: 1
```

```
如果您已安装过 Docker 服务，请输入y，否则输入n
是否进入仅执行安装程序：[y/N]y
```

```
请确认是否添加指纹：[y/N]y
```

## 2 初始化

登录

```
https://example.com:5003
```

```
用户名：admin
密码：honmashironeko
```

修改密码

## 3 使用

经典操作

![经典操作](./../../../../images/ARL/%E7%BB%8F%E5%85%B8%E6%93%8D%E4%BD%9C.png)

扫描大型网站时, `端口扫描类型` 建议修改为: `TOP100` 

 `站点截图` 容易出现卡顿

使用高并发扫描功能必须使用海外云服务器厂商提供的 VPS

```
站点爬虫
文件泄露
nuclei 调用
```

## 4 配置

将配置文件复制到本地

```shell
┌──(root㉿kali)-[~]
└─# docker cp arl_web:/code/app/config.yaml /root/config.yaml
```

修改配置文件

```shell
┌──(root㉿kali)-[~]
└─# vim /root/config.yaml
```

将配置文件复制到容器

```shell
┌──(root㉿kali)-[~]
└─# docker cp /root/config.yaml arl_web:/code/app/config.yaml
```

保存退出后打开启动程序所在路径，启动项目中的所有服务后立即重启这些服务

```shell
┌──(root㉿kali)-[~]
└─# cd /opt/ARL-docker/ && docker-compose up -d && docker-compose restart
```

> 配置好之后记得在 ARL 中刷新界面

---

参考链接

- [ARL](https://github.com/Aabyss-Team/ARL)
- [ARL 资产灯塔系统安装和使用文档](https://tophanttechnology.github.io/ARL-doc/)

