Debian is a complete Free Operating System!

## 1. Setup

- [VirtualBox](https://www.virtualbox.org/)
- [Debian](https://www.debian.org/)

## 2. Config

Move the image file to the directory

```
C:\Users\nemo\VirtualBox VMs\iso
```

Create Virtual Machine

```
> Name and Operating System
Name: debian
Folder: C:\Users\nemo\VirtualBox VMs
ISO lmage: C:\Users\nemo\VirtualBox VMs\iso\debian-amd64-DVD.iso
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
nemo
```

```
Username for your account:
nemo
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
root@debian:~# poweroff
```

## 4. Init

Port Forwarding Rules

| Name | Host Port | Guest Port |
| ---- | --------- | ---------- |
| SSH  | 60022     | 22         |
| Web  | 60080     | 80         |

Start the VM and SSH to `nemo` 

```
PS C:\Users\nemo> ssh -p 60022 nemo@127.0.0.1
```

Use `su` switch to `root` 

```
nemo@debian:~$ su - root
```

Configuring Apt Sources

```
root@debian:~# cat << 'EOF' > /etc/apt/sources.list
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian-security bookworm-security main contrib non-free non-free-firmware
EOF
```

Update the system

```
root@debian:~# apt update && apt full-upgrade \
&& apt clean && apt autoremove --purge
```

Install common tools

```
root@debian:~# apt install -y systemd-resolved passwd sudo unzip gnupg curl vim tree apache2 \
build-essential libpcap-dev mingw-w64 binutils-mingw-w64 g++-mingw-w64 \
zsh zsh-syntax-highlighting zsh-autosuggestions\
&& usermod -aG sudo nemo \
&& systemctl enable --now apache2.service
```

Keep SSH session alive

```
root@debian:~# sed -i 's/#ClientAliveInterval 0/ClientAliveInterval 60/' /etc/ssh/sshd_config \
&& sed -i 's/#ClientAliveCountMax 3/ClientAliveCountMax 60/' /etc/ssh/sshd_config
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

Configuring Network service

```
root@debian:~# systemctl disable --now NetworkManager || true \
&& systemctl enable --now networking.service \
&& systemctl enable --now systemd-networkd.service \
&& systemctl enable --now systemd-resolved.service
```

Configuring Network

```
root@debian:~# cat << 'EOF' > /etc/systemd/network/custom.network
[Match]
Name=en*

[Network]
DHCP=yes
DNS=8.8.8.8
DNS=8.8.4.4
EOF
```

Restart Network service

```
root@debian:~# systemctl restart systemd-networkd.service \
&& systemctl restart systemd-resolved.service
```

Restart

```
root@debian:~# reboot
```

Wait for the VM to start up, then Reconnect SSH

```
PS C:\Users\nemo> ssh -p 60022 nemo@127.0.0.1
```

Network testing

```
nemo@debian:~$ ping mit.edu -c 3
```

Configuring Zsh

```
nemo@debian:~$ chsh -s $(which zsh) \
&& curl -LO https://github.com/jadensalas469466/config/raw/main/Zsh/.zshrc
```

Create directory

```
nemo@debian:~$ mkdir -p ~/.local/bin \
&& sudo mkdir -p /var/www/html/exploit \
&& sudo chown -R www-data:www-data /var/www/html/exploit \
&& sudo chmod 2755 /var/www/html/exploit
```

> Grant download permissions every time a file is added to this directory
>
> ```
> ┌──(nemo@debian)-[~]
> └─# sudo chmod 644 /var/www/html/exploit/*
> ```

Take Snapshot: `init` 

```
nemo@debian:~$ sudo poweroff
```

## 5. Deploy

|                            Local                             |
| :----------------------------------------------------------: |
| [proxy](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/local/proxy) |
| [xray](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/remote/xray) |
| [proxychains-ng](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/local/proxychains-ng) |
| [git](https://keithpeck177271.gitbook.io/notes/misc/lab-env/development/git) |
| [python](https://keithpeck177271.gitbook.io/notes/misc/lab-env/language/python) |
| [go](https://keithpeck177271.gitbook.io/notes/misc/lab-env/language/go) |
| [docker](https://keithpeck177271.gitbook.io/notes/misc/lab-env/development/docker) |
| [mariadb](https://keithpeck177271.gitbook.io/notes/misc/lab-env/mariadb) |
|                         netdiscover                          |
|                           masscan                            |
|                             nmap                             |
|                           whatweb                            |
|                           wafw00f                            |
|                            katana                            |
|                          dirsearch                           |
|                            nikto                             |
|                            nuclei                            |
|                             ffuf                             |
| [metasploit-framework](https://keithpeck177271.gitbook.io/notes/general/exploit/metasploit) |
| [dvwa](https://keithpeck177271.gitbook.io/notes/misc/vuln-labs/local/web/dvwa) |
| [vulhub](https://keithpeck177271.gitbook.io/notes/misc/vuln-labs/local/docker/vulhub) |
| [vulapps](https://keithpeck177271.gitbook.io/notes/misc/vuln-labs/local/docker/vulapps) |
| [vulfocus](https://keithpeck177271.gitbook.io/notes/misc/vuln-labs/local/docker/vulfocus) |

Take Snapshot: `deploy` 

```
┌──(nemo@debian)-[~]
└─$ sudo poweroff
```

> 每台机器需要单独配置 [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) 

|                            Server                            |
| :----------------------------------------------------------: |
| [配置 SSH 密钥对连接服务器](https://keithpeck177271.gitbook.io/notes/misc/lab-env/pei-zhi-ssh-mi-yao-dui-lian-jie-fu-wu-qi) |
| [ufw](https://keithpeck177271.gitbook.io/notes/misc/security-response/firewall/ufw) |
| [fail2ban](https://keithpeck177271.gitbook.io/notes/misc/security-response/ban/fail2ban) |
| [v2ray-agent](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/remote/v2ray-agent) |
| [自建 DNS 服务器](https://keithpeck177271.gitbook.io/notes/misc/lab-env/zi-jian-dns-fu-wu-qi) |
| [配置 Syncthing 数据同步](https://keithpeck177271.gitbook.io/notes/misc/lab-env/office/data-sharing/pei-zhi-syncthing-shu-ju-tong-bu) |
| [Tor](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/remote/tor) |
| [Go](https://keithpeck177271.gitbook.io/notes/misc/lab-env/language/go) |
| [Interactsh](https://keithpeck177271.gitbook.io/notes/web/oob/interactsh) |

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
┌──(nemo@debian)-[~]
└─$ nohup <command> > ~/nohup.log 2>&1 & echo $! > ~/pid.log
```

实时查看日志

```
┌──(nemo@debian)-[~]
└─$ tail -f ~/nohup.log
```

查看 PID

```
┌──(nemo@debian)-[~]
└─$ cat  ~/pid.log
```

终止进程

```
┌──(nemo@debian)-[~]
└─$ kill -9 <PID>
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
adduser nemo
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

安装依赖

```
root@debian:~# apt install -y systemd-resolved
```

配置服务

```
root@debian:~# systemctl disable --now NetworkManager || true \
&& systemctl enable --now networking.service \
&& systemctl enable --now systemd-networkd.service \
&& systemctl enable --now systemd-resolved.service
```

动态网络

```
root@debian:~# cat << 'EOF' > /etc/systemd/network/custom.network
[Match]
Name=en*

[Network]
DHCP=yes
DNS=8.8.8.8
DNS=8.8.4.4
EOF
```

静态网络

```
root@debian:~# cat << 'EOF' > /etc/systemd/network/custom.network
[Match]
Name=en*

[Network]
Address=192.168.1.206/24
Gateway=192.168.1.1
DNS=8.8.8.8
DNS=8.8.4.4
EOF
```

重启网络配置

```
root@debian:~# systemctl restart systemd-networkd.service \
&& systemctl restart systemd-resolved.service
```

### 6.9. 安装桌面环境

安装依赖

```
root@debian:~# apt install -y gnome-shell gdm3 gnome-terminal nautilus gnome-system-monitor gnome-text-editor
```

Press Return to close this window. . .

```
Enter
```

Restart

```
root@debian:~# reboot
```

Wait for the VM to start up, then insert Guest Additions CD image

Custom Shortcuts

```
    Name: terminal
 Command: gnome-terminal
Shortcut: Ctrl + Alt +T
```

---

References

- [Debian](https://www.debian.org/)
- [Debian Docs](https://www.debian.org/doc/)

