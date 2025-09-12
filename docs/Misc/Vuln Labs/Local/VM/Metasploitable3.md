Metasploitable3 is a VM that is built from the ground up with a large amount of security vulnerabilities.

## 1. Install

- [Packer](https://developer.hashicorp.com/packer/install)
- [Vagrant](https://developer.hashicorp.com/vagrant/install)
- [VirtualBox](https://www.virtualbox.org/)

克隆仓库

```
PS C:\Users\sec\Downloads> git clone https://github.com/rapid7/metasploitable3.git
```

安装 Vagrant Reload Plugin

```
PS C:\Users\sec\Downloads> vagrant plugin install vagrant-reload
```

添加 Packer 到环境变量

```
PS C:\Users\sec\Downloads> $env:PATH += ";C:\Users\sec\Downloads\packer"
```



---

References

- [metasploitable3](https://github.com/rapid7/metasploitable3)