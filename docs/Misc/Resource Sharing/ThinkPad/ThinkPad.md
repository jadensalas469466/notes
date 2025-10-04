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
debian
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

检查缺失的驱动

```
root@debian:~# dmesg | grep -i firmware
```

Install common tools

```
root@debian:~# apt install -y systemd-resolved passwd sudo fwupd curl vim unzip tree gnupg apache2 \
zsh zsh-syntax-highlighting zsh-autosuggestions \
build-essential binutils-mingw-w64 mingw-w64 g++-mingw-w64 dkms \
libpcap-dev linux-headers-$(uname -r) \
gnome-shell gdm3 gnome-terminal nautilus gnome-text-editor \
&& usermod -aG sudo nemo \
&& systemctl disable --now apache2.service
```

Keep SSH session alive, 配置 SSH 密钥对连接

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

Custom Shortcuts

```
    Name: terminal
 Command: gnome-terminal
Shortcut: Ctrl + Alt +T
```

Wait for the VM to start up, then Reconnect SSH

```
PS C:\Users\nemo> ssh nemo@192.168.1.19
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

==加载内核驱动支持 ThinkPad 特有的功能==

```
sudo modprobe thinkpad_acpi
```

开机自动加载：在 `/etc/modules` 里加一行

```
thinkpad_acpi
```

查看特殊键按下时产生的事件

```
acpi_listen
```

检测内核是否识别 ThinkPad 驱动

```
lsmod | grep thinkpad_acpi
```

查看支持的功能

```
cat /sys/devices/platform/thinkpad_acpi/hotkey_tablet_mode
```

查看电源相关功能

```
ls /proc/acpi/ibm/
```

待装软件

```
 firefox-esr eog gnome-system-monitor
```

---

References

- [Support](https://pcsupport.lenovo.com/us/en/)
- [PSREF](https://psref.lenovo.com/)
- [Installing Debian On ThinkPad](https://wiki.debian.org/InstallingDebianOn/Thinkpad)

