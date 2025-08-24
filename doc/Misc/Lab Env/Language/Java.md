一种面向跨平台的编程语言.

## 1. Install

安装 JDK8

```
┌──(nemo@infosec)-[~]
└─$ proxychains4 curl -LO "https://github.com/adoptium/temurin8-binaries/releases/download/jdk8u462-b08/OpenJDK8U-jdk_x64_linux_hotspot_8u462b08.tar.gz" &&  sudo tar -xzvf ./OpenJDK8U* -C /usr/local && rm -rf OpenJDK8U*
```

加入环境变量

```
┌──(nemo@infosec)-[~]
└─$ sudo update-alternatives --install /usr/bin/java java /usr/local/jdk8u462-b08/bin/java 0811
```

## 2. Usage

修改 JDK

```
┌──(nemo@infosec)-[~]
└─$ update-alternatives --config java
```

```shell
There are 3 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                         Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-21-openjdk-amd64/bin/java   2111      auto mode
  1            /usr/lib/jvm/java-17-openjdk-amd64/bin/java   1711      manual mode
  2            /usr/lib/jvm/java-21-openjdk-amd64/bin/java   2111      manual mode
  3            /usr/local/jdk8u412-b08/bin/java              811       manual mode

Press <enter> to keep the current choice[*], or type selection number: 3
```

查看版本

```
┌──(nemo@infosec)-[~]
└─$ java -version
```

移除 JDK

```
┌──(nemo@infosec)-[~]
└─$ update-alternatives --remove java /usr/local/jdk8u412-b08/bin/java && rm -rf /usr/local/jdk8u412-b08/bin/java
```

---

References

- [Adoptium](https://adoptium.net/)

