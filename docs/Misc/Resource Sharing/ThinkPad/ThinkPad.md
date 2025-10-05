ThinkPad™ laptops (from Lenovo or IBM) usually work well with Debian. 

## [1. E15 Gen 4 (type 21E6 21E7) Laptops (ThinkPad)](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-edge-laptops/thinkpad-e15-gen-4-type-21e6-21e7/?linkTrack=Homepage%3ABody_Search%20Products&searchType=3&keyWordSearch=E15%20Gen%204%20%28type%2021E6%2021E7%29%20Laptops%20%28ThinkPad%29)

### 1.1. Install

Debian GNU/Linux Installer menu

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
Primary network interface:
enp
```

```
Network autoconfiguration failed
<Continue>
```

```
Network configuration method:
Do not configure the network at this time
```

```
Hostname:
xxxx-xxxx
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
/dev/
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

查看加载的网卡

```
root@debian:~# ip a
```

```
1: lo
2: enp
3: wlp
```

连接 Ethernet, 启动网卡

```
root@debian:~# ip link set enp up
```

启动 DHCP

```
root@debian:~# dhclient enp
```

查看分配的 IP

```
root@debian:~# ip a
```

```
192.168.1.19
```

### 1.2. Init

SSH to `nemo` 

```
PS C:\Users\nemo> ssh nemo@192.168.1.19
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

Install basic tools

```
root@debian:~# apt install -y systemd-resolved passwd sudo fwupd curl vim unzip tree gnupg \
zsh zsh-syntax-highlighting zsh-autosuggestions \
build-essential binutils-mingw-w64 mingw-w64 g++-mingw-w64 dkms \
libpcap-dev linux-headers-$(uname -r) \
gnome-shell gdm3 gnome-terminal nautilus \
&& usermod -aG sudo nemo
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
root@debian:~# systemctl enable NetworkManager.service || true \
&& systemctl disable networking.service \
&& systemctl disable systemd-networkd.service \
&& systemctl enable systemd-resolved.service
```

Restart

```
root@debian:~# reboot
```

Reconnect SSH

```
PS C:\Users\nemo> ssh nemo@192.168.1.19
```

Network testing

```
nemo@debian:~$ ping mit.edu -c 3
```

 [配置 SSH 密钥对连接](https://keithpeck177271.gitbook.io/notes/misc/lab-env/pei-zhi-ssh-mi-yao-dui-lian-jie)

Configuring Zsh

```
nemo@debian:~$ chsh -s $(which zsh) \
&& curl -LO https://github.com/jadensalas469466/config/raw/main/Zsh/.zshrc
```

Create directory

```
nemo@debian:~$ mkdir -p ~/.local/bin
```

加载 ThinkPad 内核驱动

```
nemo@debian:~$ sudo modprobe thinkpad_acpi
```

检查驱动更新

```
nemo@debian:~$ sudo dmesg | grep -i firmware
```

检查固件更新

```
nemo@debian:~$ sudo fwupdmgr get-updates && sudo fwupdmgr refresh
```

Install common tools

```
nemo@debian:~$ sudo apt install -y gnome-text-editor firefox-esr eog vlc \
ibus ibus-pinyin ibus-libpinyin \
&& ibus restart
```

Wi-Fi: 连接 WiFi, 自定义 IPv4 DNS 并禁用 IPv6

```
DNS: 8.8.8.8, 8.8.4.4
```

Network: 断开 Ethernet, 自定义 IPv4 DNS 并禁用 IPv6

```
DNS: 8.8.8.8, 8.8.4.4
```

Bluetooth: 关闭蓝牙

Privacy: 关闭文件历史记录, 开启自动删除垃圾内容和临时文件

Sound: 禁止声音输入

Power: 配置在插电的情况下两小时后休眠, 将电源按钮行为修改为关机, 显示电池百分比

Mouse & Touchpad: 调节鼠标和触控板的速度

Keyboard: 添加输入法 Chinese (Intelligent Pinyin), 为终端自定义快捷键

```
    Name: terminal
 Command: gnome-terminal
Shortcut: Ctrl + Alt +T
```

Removable Media: ☑ Never prompt or start programs on media insertion

Accessibility: 修改光标大小为 Medium

Default Applications: 设置默认应用

Date & Time: 修改时区

### 1.3. Deploy

|                                             Laptop                                             |
| :-------------------------------------------------------------------------------------------: |
|         [proxy](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/local/proxy)         |
|         [xray](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/remote/xray)          |
| [proxychains-ng](https://keithpeck177271.gitbook.io/notes/misc/lab-env/proxy/tools/local/proxychains-ng) |
|           [aria2](https://keithpeck177271.gitbook.io/notes/misc/lab-env/office/download/aria2)           |
|               [git](https://keithpeck177271.gitbook.io/notes/misc/lab-env/development/git)               |
|             [python](https://keithpeck177271.gitbook.io/notes/misc/lab-env/language/python)              |
|                 [go](https://keithpeck177271.gitbook.io/notes/misc/lab-env/language/go)                  |
|            [docker](https://keithpeck177271.gitbook.io/notes/misc/lab-env/development/docker)            |
|                                       [AppImageLauncher]                                        |
|                                            [vnote]                                             |

|                             test                             |
| :----------------------------------------------------------: |
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

---

References

- [Support](https://pcsupport.lenovo.com/us/en/)
- [PSREF](https://psref.lenovo.com/)
- [Installing Debian On ThinkPad](https://wiki.debian.org/InstallingDebianOn/Thinkpad)

