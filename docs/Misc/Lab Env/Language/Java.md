一种面向跨平台的编程语言.

## 1. Install

安装 JDK8

```
┌──(nemo@debian)-[~]
└─$ curl -LO "https://github.com/adoptium/temurin8-binaries/releases/download/jdk8u462-b08/OpenJDK8U-jdk_x64_linux_hotspot_8u462b08.tar.gz" \
&& tar -xzvf ./OpenJDK8U-jdk* -C ~/.local/ \
&& rm -f ./OpenJDK8U-jdk*
```

加入环境变量

```
┌──(nemo@debian)-[~]
└─$ sudo update-alternatives --install /usr/bin/java java ~/.local/jdk8u462-b08/bin/java 0811
```

## 2. Usage

修改 JDK

```
┌──(nemo@debian)-[~]
└─$ sudo update-alternatives --config java
```

```shell
There are 3 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                         Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-21-openjdk-amd64/bin/java   2111      auto mode
  1            /usr/lib/jvm/java-17-openjdk-amd64/bin/java   1711      manual mode
  2            /usr/lib/jvm/java-21-openjdk-amd64/bin/java   2111      manual mode
  3            /home/nemo/.local/jdk8u462-b08/bin/java       811       manual mode

Press <enter> to keep the current choice[*], or type selection number: 3
```

查看版本

```
┌──(nemo@debian)-[~]
└─$ java -version
```

移除 JDK

```
┌──(nemo@debian)-[~]
└─$ sudo update-alternatives --remove java ~/.local/jdk8u462-b08/bin/java \
&& rm -rf ~/.local/jdk8u462-b08/
```

---

References

- [Adoptium](https://adoptium.net/)
- [temurin8-binaries](https://github.com/adoptium/temurin8-binaries)

