一种面向跨平台的编程语言.111

## 1. Step

### 1.1. Debian

导入 GPG 密钥

```
┌──(nemo@debian)-[~]
└─$ sudo mkdir -p /etc/apt/keyrings \
&& curl -fsSL https://packages.adoptium.net/artifactory/api/gpg/key/public | sudo tee /etc/apt/keyrings/adoptium.asc
```

添加 Adoptium 仓库

```
┌──(nemo@debian)-[~]
└─$ echo "deb [signed-by=/etc/apt/keyrings/adoptium.asc arch=amd64] https://packages.adoptium.net/artifactory/deb $(lsb_release -c -s) main" | sudo tee /etc/apt/sources.list.d/adoptium.list
```

获取更新

```
┌──(nemo@debian)-[~]
└─$ sudo apt update
```

### 1.2. Windows

[Temurin JRE 8](https://adoptium.net/temurin/releases?version=8&os=any&arch=any)

[Liberica Full JDK 11](https://bell-sw.com/pages/downloads/#jdk-11-lts)

## 2. Install

### 2.1. Debian

安装 JDK

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y temurin-8-jdk temurin-11-jdk
```

## 3. Usage

### 3.1. Debian

修改 JDK 版本

```
┌──(nemo@debian)-[~]
└─$ sudo update-alternatives --config java
```

```shell
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                        Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/temurin-11-jdk-amd64/bin/java   1111      auto mode
  1            /usr/lib/jvm/temurin-11-jdk-amd64/bin/java   1111      manual mode
  2            /usr/lib/jvm/temurin-8-jdk-amd64/bin/java    1081      manual mode

Press <enter> to keep the current choice[*], or type selection number: 2
```

查看版本

```
┌──(nemo@debian)-[~]
└─$ java -version
```

运行 JAR

```
┌──(nemo@debian)-[~]
└─$ java -jar ./app.jar
```

### 3.2. Windows

指定版本运行 JAR

```
C:\Program Files\BellSoft\LibericaJDK-11-Full\bin\javaw.exe
```

![切换版本运行](./../../../../images/Java/%E5%88%87%E6%8D%A2%E7%89%88%E6%9C%AC%E8%BF%90%E8%A1%8C.png)

---

References

- [Temurin](https://adoptium.net/temurin/releases)
- [Liberica](https://bell-sw.com/pages/downloads/)

