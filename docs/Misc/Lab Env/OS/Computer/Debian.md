Debian is a complete Free Operating System!

## 1. Setup

- [VirtualBox](https://www.virtualbox.org/)
- [Debian](https://www.debian.org/)

## 2. Config

Move the image file to the directory

```
C:\Users\nemo\VirtualBox VMs\iso
```

New Virtual Machine

```
> Virtual machine name and operating system
VM Name: debian
VM Folder: C:\Users\nemo\VirtualBox VMs
ISO lmage: C:\Users\nemo\VirtualBox VMs\iso\debian-amd64-DVD.iso
OS: Linux
OS Distribution: Debian
OS Version: Debian (64-bit)
☐ Proceed with Unattended Installation

> Specify virtual hardware
Base Memory: 4096 MB
Number of CPUs: 1 CPU

> Specify virtual hard disk
Hard Disk File Location and Size: C:\Users\nemo\VirtualBox VMs\debian\debian.vdi
Disk Size: 64.00GB
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
English - English
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
VBOX HARDDISK
```

```
Partitioning scheme:
All files in one partition
```

```
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
VBOX_HARDDISK
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

Switch to `root` 

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
root@debian:~# apt install -y systemd-resolved passwd sudo curl vim unzip tree gnupg apache2 \
zsh zsh-syntax-highlighting zsh-autosuggestions \
build-essential binutils-mingw-w64 mingw-w64 g++-mingw-w64 dkms \
libpcap-dev linux-headers-$(uname -r) \
&& usermod -aG sudo nemo \
&& systemctl enable --now apache2.service
```

Keep SSH session alive

```
root@debian:~# sed -i 's/#ClientAliveInterval 0/ClientAliveInterval 60/' /etc/ssh/sshd_config \
&& sed -i 's/#ClientAliveCountMax 3/ClientAliveCountMax 60/' /etc/ssh/sshd_config \
&& systemctl reload ssh.service
```

Configuring Zsh

```
root@debian:~# chsh -s $(which zsh) \
&& curl -LO https://github.com/jadensalas469466/config/raw/main/Zsh/.zshrc
```

Configuring Network service

```
root@debian:~# systemctl disable --now NetworkManager || true \
&& systemctl disable networking.service \
&& systemctl enable systemd-networkd.service \
&& systemctl enable systemd-resolved.service
```

Configuring Network

```
root@debian:~# cat << 'EOF' > /etc/systemd/network/custom.network
[Match]
Name=en*

[Network]
DHCP=yes
IPv6AcceptRA=no
DNS=8.8.8.8
DNS=8.8.4.4
EOF
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
| [subfinder](https://keithpeck177271.gitbook.io/notes/web/recon/subdomain/subfinder) |
| [dnsx](https://keithpeck177271.gitbook.io/notes/web/recon/dns/dnsx) |
| [cdncheck](https://keithpeck177271.gitbook.io/notes/web/recon/cdn/cdncheck) |
| [naabu](https://keithpeck177271.gitbook.io/notes/web/recon/port/naabu) |
| [masscan](https://keithpeck177271.gitbook.io/notes/web/recon/port/masscan) |
| [nmap](https://keithpeck177271.gitbook.io/notes/web/recon/port/nmap) |
| [httpx](https://keithpeck177271.gitbook.io/notes/web/recon/http-status/httpx) |
| [whatweb](https://keithpeck177271.gitbook.io/notes/web/recon/fingerprint/service/whatweb) |
| [wafw00f](https://keithpeck177271.gitbook.io/notes/web/recon/fingerprint/waf/wafw00f) |
| [trufflehog](https://keithpeck177271.gitbook.io/notes/web/info-disclosure/trufflehog) |
| [ffuf](https://keithpeck177271.gitbook.io/notes/web/fuzz/ffuf) |
| [interactsh](https://keithpeck177271.gitbook.io/notes/web/oob/interactsh) |
| [nuclei](https://keithpeck177271.gitbook.io/notes/web/scan/active/nuclei) |
| [hydra](https://keithpeck177271.gitbook.io/notes/crypto/brute-force/hydra) |
| [medusa](https://keithpeck177271.gitbook.io/notes/crypto/brute-force/medusa) |
| [metasploit-framework](https://keithpeck177271.gitbook.io/notes/general/exploit/metasploit-framework) |
| [frp](https://keithpeck177271.gitbook.io/notes/system/nat-traversal/frp) |
| [sliver](https://keithpeck177271.gitbook.io/notes/system/c2/sliver) |
| [netdiscover](https://keithpeck177271.gitbook.io/notes/system/lan-discovery/netdiscover) |
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
| [配置 Syncthing 文件同步](https://keithpeck177271.gitbook.io/notes/misc/lab-env/office/data-sharing/pei-zhi-syncthing-shu-ju-tong-bu) |
| [tor](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/remote/tor) |
| [proxychains-ng](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/local/proxychains-ng) |
| [frp](https://keithpeck177271.gitbook.io/notes/system/nat-traversal/frp) |
| [sliver](https://keithpeck177271.gitbook.io/notes/system/c2/sliver) |
| [metasploit-framework](https://keithpeck177271.gitbook.io/notes/general/exploit/metasploit-framework) |

## 6. Usage

### 6.1. 安装桌面环境

安装依赖

```
root@debian:~# apt install -y gnome-shell gdm3 gnome-terminal nautilus gnome-system-monitor gnome-text-editor
```

Restart

```
root@debian:~# reboot
```

Wait for the VM to start up, then insert Guest Additions CD image

挂载增强工具

```
┌──(nemo@debian)-[~]
└─$ sudo mount /dev/cdrom /mnt
```

安装增强工具

```
┌──(nemo@debian)-[~]
└─$ sudo bash /mnt/VBoxLinuxAdditions.run
```

Custom Shortcuts

```
    Name: terminal
 Command: gnome-terminal
Shortcut: Ctrl + Alt +T
```

### 6.2. 配置无线网卡驱动

下载驱动

```
┌──(nemo@debian)-[~]
└─$ git clone https://github.com/aircrack-ng/rtl8812au.git
```

安装驱动

```
┌──(nemo@debian)-[~]
└─$ cd ./rtl8812au && sudo make dkms_install
```

卸载驱动

```
┌──(nemo@debian)-[~]
└─$ cd ./rtl8812au && sudo make dkms_remove
```

### 6.3. 挂载共享文件

安装增强工具后设置共享文件夹 `Share Folder` 并创建挂载目录

```
┌──(nemo@debian)-[~]
└─$ mkdir -p ~/share
```

挂载共享文件夹

```
┌──(nemo@debian)-[~]
└─$ sudo mount -t vboxsf <Share Folder> ~/share
```

取消挂载

```
┌──(nemo@debian)-[~]
└─$ sudo umount ~/share
```

### 6.4. 历史命令

擦除历史命令

```
┌──(nemo@debian)-[~]
└─# shred -z ~/.bash_history ~/.zsh_history
```

### 6.5. 后台运行

将命令行程序放在后台运行, 即使 SSH 断开连接也不会终止运行

```
┌──(nemo@debian)-[~]
└─$ nohup <command> > ~/<command>-nohup.log 2>&1 &
echo $! > ~/<command>-pid.log
```

实时查看日志

```
┌──(nemo@debian)-[~]
└─$ tail -f ~/<command>-nohup.log
```

查看 PID

```
┌──(nemo@debian)-[~]
└─$ cat ~/<command>-pid.log
```

终止进程

```
┌──(nemo@debian)-[~]
└─$ kill -15 <PID> # 请求终止

┌──(nemo@debian)-[~]
└─$ kill -9 <PID>  # 强制终止
```

### 6.6. SSH 配置

SSH 配置文件

```
root@debian:~# sudo nano -l /etc/ssh/sshd_config
```

root 用户登录 (默认允许以密钥对登录)

```
33 #PermitRootLogin prohibit-password # 允许 root 用户以密钥对登录
33 PermitRootLogin prohibit-password  # 允许 root 用户以密钥对登录
33 PermitRootLogin yes                # 允许 root 用户以密钥对或密码登录
33 PermitRootLogin no                 # 禁止 root 用户登录
```

普通用户密钥对登录 (默认允许以密钥对登录)

```
38 #PubkeyAuthentication yes # 允许普通用户以密钥对登录
38 PubkeyAuthentication yes  # 允许普通用户以密钥对登录
```

普通用户密码登录 (默认允许以密码登录)

```
57 #PasswordAuthentication yes # 允许普通用户以密码登录
57 PasswordAuthentication no   # 禁止普通用户以密码登录
```

重启 SSH 服务

```
root@debian:~# systemctl restart ssh.service
```

### 6.7. 配置网络

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
&& systemctl disable networking.service \
&& systemctl enable systemd-networkd.service \
&& systemctl enable systemd-resolved.service
```

动态网络

```
root@debian:~# cat << 'EOF' > /etc/systemd/network/custom.network
[Match]
Name=en*

[Network]
DHCP=yes
IPv6AcceptRA=no
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
IPv6AcceptRA=no
DNS=8.8.8.8
DNS=8.8.4.4
EOF
```

Restart

```
root@debian:~# reboot
```

### 6.9. 创建链接

创建软链接以全局运行

```
┌──(nemo@debian)-[~]
└─$ ln -sf ~/.local/bin/app /usr/local/bin/app
```

---

References

- [Debian](https://www.debian.org/)
- [Debian Docs](https://www.debian.org/doc/)

