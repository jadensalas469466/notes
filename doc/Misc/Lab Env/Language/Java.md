一种面向跨平台的编程语言.

## 1 安装

安装 jdk8

```shell
┌──(root㉿kali)-[~]
└─# proxychains4 wget 'https://github.com/adoptium/temurin8-binaries/releases/download/jdk8u412-b08/OpenJDK8U-jdk_x64_linux_hotspot_8u412b08.tar.gz' &&  tar -xzvf OpenJDK8U-jdk_x64_linux_hotspot_8u412b08.tar.gz -C /usr/local && rm -rf OpenJDK8U-jdk_x64_linux_hotspot_8u412b08.tar.gz
```

加入环境变量

```shell
┌──(root㉿a-kali-23)-[~]
└─# update-alternatives --install /usr/bin/java java /usr/local/jdk8u412-b08/bin/java 0804
```

## 2 使用

修改 jdk

```shell
┌──(root㉿kali)-[~]
└─# update-alternatives --config java
```

```shell
There are 3 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                         Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-21-openjdk-amd64/bin/java   2111      auto mode
  1            /usr/lib/jvm/java-17-openjdk-amd64/bin/java   1711      manual mode
  2            /usr/lib/jvm/java-21-openjdk-amd64/bin/java   2111      manual mode
  3            /usr/local/jdk8u412-b08/bin/java              804       manual mode

Press <enter> to keep the current choice[*], or type selection number: 3
```

> 或者一键更改
>
> ```shell
> ┌──(root㉿kali)-[~]
> └─# sudo update-alternatives --set java /usr/local/jdk8u412-b08/bin/java
> ```

查看版本

```shell
┌──(root㉿a-kali-23)-[~]
└─# java -version
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
openjdk version "1.8.0_412"
OpenJDK Runtime Environment (Temurin)(build 1.8.0_412-b08)
OpenJDK 64-Bit Server VM (Temurin)(build 25.412-b08, mixed mode)
```

移除 jdk

```shell
┌──(root㉿kali)-[~]
└─# update-alternatives --remove java /usr/local/jdk8u412-b08/bin/java && rm -rf /usr/local/jdk8u412-b08/bin/java
```

---

References

- [Adoptium](https://adoptium.net/)

