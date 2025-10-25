debian 遇到的问题  
  
使用 IBus 的中文输入法时中英文呢混合输入会出现问题 , 改用 Fcitx5

安装 Fcitx5

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y --install-recommends fcitx5 fcitx5-chinese-addons fcitx5-pinyin gnome-shell-extension-kimpanel
```

```
gnome-extensions enable kimpanel@kde.org
```

```
cat << 'EOF' > ~/.pam_environment
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
EOF
```

```
im-config -n fcitx5
```

重启

```
┌──(nemo@debian)-[~]
└─$ sudo reboot
```