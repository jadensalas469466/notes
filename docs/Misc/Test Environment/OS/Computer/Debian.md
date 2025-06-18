Debian is a complete Free Operating System!

## 1. Setup

debian-12.11.0-amd64-DVD-1.iso

```
https://www.debian.org/distrib/
```

VMware Workstation Pro

```
https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion
```

Directory

```
C:\Users\sec\Documents\Virtual Machines\debian
```

## 2. Config

移动镜像文件到 `iso` 文件夹

```
C:\Users\sec\Documents\Virtual Machines\iso
```

VMware Workstation Pro

```
创建新的虚拟机
```

您希望使用什么类型的配置？

```
自定义
```

硬件兼容性

```
Workstation 17.5 or later
```

安装来源

```
稍后安装操作系统
```

客户机操作系统

```
Linux
```

版本

```
Debian 12.x 64 位
```

虚拟机名称

```
debian
```

位置

```
C:\Users\sec\Documents\Virtual Machines\debian
```

处理器数量

```
1
```

每个处理器的内核数量

```
2
```

此虚拟机的内存

```
4096 MB
```

网络连接

```
使用桥接网络
```

SCSI 控制器

```
LSI Logic
```

虚拟磁盘类型

```
SCSI
```

磁盘

```
创建新虚拟磁盘
```

最大磁盘大小

```
64.0 GB
```

```
将虚拟磁盘存储为单个文件
```

磁盘文件

```
C:\Users\sec\Documents\Virtual Machines\debian\debian.vmdk
```

编辑虚拟机设置

处理器

```
虚拟化引擎
虚拟化 Intel VT-x/EPT 或 AMD-V/RVI
```

CD/DVD

```
使用 ISO 映像文件
C:\Users\sec\Documents\Virtual Machines\iso\debian-12.10.0-amd64-DVD-1.iso
```

拍摄快照并命名为 `config` 

## 3. Install

开启此虚拟机进行安装

Debian GNU/Linux installer menu

```
Install
```

Select a language

```
Language:
English
```

Select your location

```
Country, territory or area:
United States
```

Configure the keyboard

```
Keymap to use:
American English
```

Configure the network

```
Hostname:
debian
```

```
Domain name:
```

Set up users and passwords

```
Root password:
123456
```

```
Re-enter password to verify:
123456
```

```
Full name for the new user:
sec
```

```
Username for your account:
sec
```

```
Choose a password for the new user:
123456
```

```
Re-enter password to verify:
123456
```

Configure the clock

```
Select a location in your time zone:
Eastern
```

Partition disks

```
Partitioning method:
Guided - use entire disk
```

```
Select disk to partition:
Default
```

```
Partitioning scheme:
All files in one partition
```

```
Select a partitions to modify its settings
Finish partitioning and write changes to disk
```

```
Write the changes to disks?
<Yes>
```

Configure the package manager

```
Scan extra installation media?
<No>
```

```
Use a network mirror?
<No>
```

Configuring popularity- contest

```
Participate in the package usage survey?
<No>
```

Software selection

```
Choose software to install:
[*] SSH server
[*] standard system utilities
```

Configuring grub-pc

```
Install the GRUB boot loader to your primary drive?
<Yes>
```

```
Device for boot loader installation:
/dev/
```

Finish the installation

```
Please choose <Continue> to reboot.
<Continue>
```

登录

```
debian login: root
Password: 123456
```

查看 IP 和网卡

```
root@debian:~# ip a
```

关机，拍摄快照并命名为 `install` 

```
root@debian:~# shutdown -h now
```

## 4. Init

启动虚拟机，使用 SSH 登录 `sec` 用户

```
PS C:\Users\sec> ssh sec@<ip>
```

切换到 `root` 用户

```
sec@debian:~$ su - root
```

配置 `apt` 源

```
root@debian:~# nano /etc/apt/sources.list
```

```
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian-security bookworm-security main contrib non-free non-free-firmware
```

更新系统

```
root@debian:~# apt update && apt full-upgrade \
&& apt clean && apt autoremove --purge
```

安装常用工具

```
root@debian:~# apt install -y vim curl passwd sudo tree unzip apache2 build-essential libpcap-dev mingw-w64 binutils-mingw-w64 g++-mingw-w64 \
zsh zsh-syntax-highlighting zsh-autosuggestions \
&& systemctl disable --now apache2.service \
&& usermod -aG sudo sec
```

配置 SSH 稳定连接

```
root@debian:~# nano -l /etc/ssh/sshd_config
```

```
 99 ClientAliveInterval 60
100 ClientAliveCountMax 60
```

重启 SSH 服务

```
root@debian:~# systemctl restart ssh.service
```

配置 Zsh

```
root@debian:~# chsh -s $(which zsh) \
&& curl -LO https://github.com/jadensalas469466/config/raw/main/Zsh/.zshrc
```

配置网络

```
root@debian:~# systemctl disable NetworkManager --now || true && systemctl enable systemd-networkd.service --now && nano /etc/systemd/network/static.network
```

```
[Match]
Name=ens33

[Network]
Address=192.168.1.203/24
Gateway=192.168.1.1
DNS=8.8.8.8
DNS=8.8.4.4
```

修改 DNS 配置

```
root@debian:~# echo "supersede domain-name-servers 8.8.8.8, 8.8.4.4;" >> /etc/dhcp/dhclient.conf
```

在 `hosts` 文件添加域名映射

```
root@debian:~# cat <<'EOF'>> /etc/hosts

192.168.1.203     debian.local
EOF
```

重启

```
root@debian:~# shutdown -r now
```

在 Powershell 中删除 SSH 连接缓存

```
PS C:\Users\sec> ssh-keygen -R <ip>
```

等待虚拟机启动, 重新连接 SSH

```
PS C:\Users\sec> ssh sec@debian.local
```

测试网络

```
sec@debian:~$ ping mit.edu -c 3
```

配置 Zsh

```
sec@debian:~$ chsh -s $(which zsh) \
&& curl -LO https://github.com/jadensalas469466/config/raw/main/Zsh/.zshrc
```

创建目录并配置权限

```
sec@debian:~$ sudo mkdir -p /var/www/html/exploit \
&& sudo chown -R www-data:www-data /var/www/html/exploit \
&& sudo chmod 2755 /var/www/html/exploit
```

> 每次在 `/var/www/html/exploit/` 中加入文件后都要授予下载权限
>
> ```
> ┌──(sec@debian)-[~]
> └─# sudo chmod 644 /var/www/html/exploit/*
> ```

关机，拍摄快照并命名为 `init` 

```
sec@debian:~$ sudo shutdown -h now
```

## 5. Deploy

|                             env                              |
| :----------------------------------------------------------: |
| [proxy](https://github.com/jadensalas469466/tools/raw/main/other/proxy.sh) |
|               [xray](https://xtls.github.io/)                |
| [proxychains-ng](https://www.kali.org/tools/proxychains-ng/) |
|                 [Git](https://git-scm.com/)                  |
|              [Python](https://www.python.org/)               |
|                    [Go](https://go.dev/)                     |
|              [Docker](https://www.docker.com/)               |
|               [MariaDB](https://mariadb.org/)                |

|                            tools                            |
| :---------------------------------------------------------: |
|         [whois](https://www.kali.org/tools/whois/)          |
|       [masscan](https://www.kali.org/tools/masscan/)        |
|          [nmap](https://www.kali.org/tools/nmap/)           |
|     [dirsearch](https://www.kali.org/tools/dirsearch/)      |
|       [whatweb](https://www.kali.org/tools/whatweb/)        |
|       [wafw00f](https://www.kali.org/tools/wafw00f/)        |
|         [nikto](https://www.kali.org/tools/nikto/)          |
|         [hydra](https://www.kali.org/tools/hydra/)          |
|        [medusa](https://www.kali.org/tools/medusa/)         |
|          [metasploit](https://www.metasploit.com/)          |
| [subfinder](https://github.com/projectdiscovery/subfinder)  |
|     [naabu](https://github.com/projectdiscovery/naabu)      |
|     [httpx](https://github.com/projectdiscovery/httpx)      |
|    [katana](https://github.com/projectdiscovery/katana)     |
|   [mapcidr](https://github.com/projectdiscovery/mapcidr)    |
|    [nuclei](https://github.com/projectdiscovery/nuclei)     |
| [trufflehog](https://github.com/trufflesecurity/trufflehog) |
|            [ffuf](https://github.com/ffuf/ffuf)             |
|        [sqlmap](https://www.kali.org/tools/sqlmap/)         |
|        [sliver](https://github.com/BishopFox/sliver)        |

关机，拍摄快照并命名为 `deploy` 

```
sec@debian:~$ sudo shutdown -h now
```

|                            server                            |
| :----------------------------------------------------------: |
| [配置 SSH 密钥对连接服务器](https://keithpeck177271.gitbook.io/notes/misc/test_environment/pei-zhi-ssh-mi-yao-dui-lian-jie-fu-wu-qi) |
|              [ufw](https://github.com/jbq/ufw)               |
|       [fail2ban](https://github.com/fail2ban/fail2ban)       |
| [搭建 VLESS+Reality+uTLS+Vision 高匿代理](https://keithpeck177271.gitbook.io/notes/misc/proxy/tools/remote/da-jian-vless+reality+utls+vision-gao-ni-dai-li) |
| [自建 DNS 服务器](https://keithpeck177271.gitbook.io/notes/misc/test-environment/zi-jian-dns-fu-wu-qi) |
| [配置 Syncthing 数据同步](https://keithpeck177271.gitbook.io/notes/misc/test-environment/management-tools/shu-ju-guan-li/shu-ju-tong-bu/pei-zhi-syncthing-shu-ju-tong-bu) |
|              [Tor](https://www.torproject.org/)              |
|          [metasploit](https://www.metasploit.com/)           |
|        [sliver](https://github.com/BishopFox/sliver)         |

## 6. Usage

### 6.1. 配置无线网卡驱动

查看内核版本

```
┌──(root@debian)-[~]
└─# uname -r
6.5.0-kali3-amd64
```

安装对应的版本

> http://http.kali.org/kali/pool/main/l/linux/

```
┌──(root@debian)-[~]
└─# wget http://http.kali.org/kali/pool/main/l/linux/linux-compiler-gcc-13-x86_6.5.13-1kali2_amd64.deb \
&& dpkg -i linux-compiler-gcc-13-x86_6.5.13-1kali2_amd64.deb \
&& rm -rf linux-compiler-gcc-13-x86_6.5.13-1kali2_amd64.deb
```

安装依赖

```
┌──(root@debian)-[~]
└─# apt install -y build-essential dkms
```

下载驱动

```
┌──(root@debian)-[~]
└─# git clone https://github.com/aircrack-ng/rtl8812au.git /root/tools/drivers/rtl8812au
```

安装驱动

```
┌──(root@debian)-[~]
└─# cd /root/tools/drivers/rtl8812au \
&& make dkms_install \
&& cd
```

> 卸载
>
> ```
> root@debian:~# cd /root/tools/drivers/rtl8812au \
> && make dkms_remove \
> && cd
> ```

### 6.2. 系统信息

查看内核版本

```
uname -r
```

### 6.3. 挂载共享文件

创建目录

```
┌──(root@debian)-[~]
└─# mkdir -p /mnt/vmware
```

配置别名

```
┌──(root@debian)-[~]
└─# echo "alias share='vmhgfs-fuse .host:/ /mnt/vmware'" >> ~/.zshrc && source ~/.zshrc
```

### 6.4. 历史命令

擦除历史命令

```
┌──(root@debian)-[~]
└─# shred -z ~/.bash_history \
&& shred -z ~/.zsh_history
```

### 6.5. 后台运行

将命令行程序放在后台运行, 即使 SSH 断开连接也不会终止运行

```
nohup <command> > /root/log.txt 2>&1 &
```

```
PID
```

查看后台程序

```
jobs
```

> 在当前终端关闭后将失效

实时查看日志

```
tail -f /root/log.txt
```

终止进程

```
kill -9 <PID>
```

### 6.6. 配置全局代理

配置代理

```
export http_proxy=http://ip:port && \
export https_proxy=$http_proxy
```

取消代理

```
unset http_proxy && \
unset https_proxy
```

### 6.7. 创建用户

创建一个普通用户

```
adduser sec
```

### 6.8. SSH 相关配置

SSH 配置文件

```
nano -l /etc/ssh/sshd_config
```

使用 root 登录 (默认禁止)

```
33 #PermitRootLogin prohibit-password # 禁止以 root 身份登录
33 PermitRootLogin prohibit-password  # 允许 root 以密钥登录
33 PermitRootLogin yes                # 允许 root 以密码登录
```

密钥对登录 (默认禁止)

```
38 #PubkeyAuthentication yes
```

密码登录 (默认允许)

```
57 #PasswordAuthentication yes
```

重启 SSH 服务

```
root@debian:~# systemctl restart ssh.service
```

---

Refrences

- [Debian](https://www.debian.org/)
- [Debian Docs](https://www.debian.org/doc/)

