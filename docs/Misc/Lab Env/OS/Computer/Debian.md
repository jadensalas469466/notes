Debian is a complete Free Operating System!

## 1. Setup

- [VirtualBox](https://www.virtualbox.org/)
- [Debian](https://www.debian.org/)

## 2. Config

Move the image file to the directory

```
C:\Users\sec\VirtualBox VMs\iso
```

Create Virtual Machine

```
> Name and Operating System
Name: debian
Folder: C:\Users\sec\VirtualBox VMs
ISO lmage: C:\Users\sec\VirtualBox VMs\iso\debian-amd64-DVD-1.iso
Version: Debian (64-bit)
☑ Skip Unattended Installation

> Hardware
Base Memory: 4096 MB
Processors: 1 CPU

> Hard Disk
Hard Disk File Size: 64.00GB
```

Take Snapshot: `config` 

## 3. Install

Start the VM to install

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
Select your time zone:
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
Default
```

Finish the installation

```
Please choose <Continue> to reboot.
<Continue>
```

Login

```
debian login: root
Password: 123456
```

Take Snapshot: `install` 

```
root@debian:~# shutdown -h now
```

## 4. Init

Port Forwarding Rules

| Name | Host Port | Guest Port |
| ---- | --------- | ---------- |
| SSH  | 60022     | 22         |
| Web  | 60080     | 80         |

Start the VM and SSH to `sec` 

```
PS C:\Users\sec> ssh -p 60022 sec@127.0.0.1
```

Use `su` switch to `root` 

```
sec@debian:~$ su - root
```

Configuring Apt Sources

```
root@debian:~# nano /etc/apt/sources.list
```

```
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian-security bookworm-security main contrib non-free non-free-firmware
```

Update the system

```
root@debian:~# apt update && apt full-upgrade \
&& apt clean && apt autoremove --purge
```

Install common tools

```
root@debian:~# apt install -y vim curl passwd sudo tree unzip apache2 build-essential libpcap-dev mingw-w64 binutils-mingw-w64 g++-mingw-w64 \
zsh zsh-syntax-highlighting zsh-autosuggestions \
&& systemctl enable --now apache2.service \
&& usermod -aG sudo sec
```

Keep SSH session alive

```
root@debian:~# nano -l /etc/ssh/sshd_config
```

```
 99 ClientAliveInterval 60
100 ClientAliveCountMax 60
```

Restart SSH service

```
root@debian:~# systemctl restart ssh.service
```

Configuring Zsh

```
root@debian:~# chsh -s $(which zsh) \
&& curl -LO https://github.com/jadensalas469466/config/raw/main/Zsh/.zshrc
```

Configuring Network

```
root@debian:~# systemctl disable NetworkManager --now || true && systemctl enable networking.service --now
```

Change DNS servers

```
root@debian:~# nano /etc/resolv.conf
```

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

Restart

```
root@debian:~# shutdown -r now
```

Wait for the VM to start up, then reconnect SSH

```
PS C:\Users\sec> ssh -p 60022 sec@127.0.0.1
```

Network testing

```
sec@debian:~$ ping mit.edu -c 3
```

Configuring Zsh

```
sec@debian:~$ chsh -s $(which zsh) \
&& curl -LO https://github.com/jadensalas469466/config/raw/main/Zsh/.zshrc
```

Create directory

```
sec@debian:~$ sudo mkdir -p /var/www/html/exploit \
&& sudo chown -R www-data:www-data /var/www/html/exploit \
&& sudo chmod 2755 /var/www/html/exploit
```

> Grant download permissions every time a file is added to this directory
>
> ```
> ┌──(sec@debian)-[~]
> └─# sudo chmod 644 /var/www/html/exploit/*
> ```

Take Snapshot: `init` 

```
sec@debian:~$ sudo shutdown -h now
```

## 5. Deploy

|                            local                             |
| :----------------------------------------------------------: |
| [proxy](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/remote/proxy) |
| [xray](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/remote/xray) |
| [proxychains-ng](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/remote/proxychains-ng) |
| [git](https://keithpeck177271.gitbook.io/notes/misc/lab-env/development/git) |
| [python](https://keithpeck177271.gitbook.io/notes/misc/lab-env/language/python/python) |
| [go](https://keithpeck177271.gitbook.io/notes/misc/lab-env/language/go) |
| [docker](https://keithpeck177271.gitbook.io/notes/misc/lab-env/development/docker) |
| [mariadb](https://keithpeck177271.gitbook.io/notes/misc/lab-env/mariadb) |
| [dvwa](https://keithpeck177271.gitbook.io/notes/misc/vuln-labs/local/web/dvwa) |
| [vulfocus](https://keithpeck177271.gitbook.io/notes/misc/vuln-labs/local/docker/vulfocus) |
| [sqlmap](https://keithpeck177271.gitbook.io/notes/web/fuzz/sqli/sqlmap) |
| [xsstrike](https://keithpeck177271.gitbook.io/notes/web/fuzz/xss/xsstrike) |

Take Snapshot: `deploy` 

```
┌──(sec@debian)-[~]
└─$ sudo shutdown -h now
```

> 每台机器需要单独配置 [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)

|                            server                            |
| :----------------------------------------------------------: |
| [配置 ssh 密钥对连接服务器](https://keithpeck177271.gitbook.io/notes/misc/lab-env/pei-zhi-ssh-mi-yao-dui-lian-jie-fu-wu-qi) |
| [ufw](https://keithpeck177271.gitbook.io/notes/misc/security-response/firewall/ufw) |
| [fail2ban](https://keithpeck177271.gitbook.io/notes/misc/security-response/ban/fail2ban) |
| [v2ray-agent](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/remote/da-jian-gao-ni-dai-li) |
| [自建 DNS 服务器](https://keithpeck177271.gitbook.io/notes/misc/lab-env/zi-jian-dns-fu-wu-qi) |
| [配置 Syncthing 数据同步](https://keithpeck177271.gitbook.io/notes/misc/lab-env/office/data-sharing/pei-zhi-syncthing-shu-ju-tong-bu) |
| [tor](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/remote/tor) |

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

### 6.8. 配置网络

查看网络接口

```
root@debian:~# ip link
```

为指定接口配置静态 IP

```
root@debian:~# systemctl disable NetworkManager --now || true && systemctl enable networking.service --now && nano -l /etc/network/interfaces
```

```
10  # The primary network interface
11  allow-hotplug ens33
12  # iface ens33 inet dhcp
auto ens33
iface ens33 inet static
    address 192.168.1.6
    gateway 192.168.1.1
    netmask 255.255.255.0
18  # This is an autoconfigured IPv6 interface
19  # iface ens33 inet6 auto
```

配置 DNS 服务器

```
root@debian:~# nano /etc/resolv.conf
```

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

---

References

- [Debian](https://www.debian.org/)
- [Debian Docs](https://www.debian.org/doc/)

