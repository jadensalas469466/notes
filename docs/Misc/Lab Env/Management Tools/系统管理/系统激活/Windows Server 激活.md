卸载产品密钥

```cmd
C:\Users\sec>slmgr.vbs -upk
```

查找[产品密钥](https://learn.microsoft.com/zh-cn/windows-server/get-started/kms-client-activation-keys#windows-server-2008-r2)

```
Windows Server 2008 R2 Datacenter
74YFP-3QFB3-KQT8W-PMXWJ-7M648
```

```
Windows Server 2022 Datacenter
WX4NM-KYWYW-QJJR4-XV3QB-6VM33
```

安装产品密钥

```cmd
C:\Users\sec>slmgr.vbs /ipk 74YFP-3QFB3-KQT8W-PMXWJ-7M648
```

查找 [KMS](https://www.coolhub.top/tech-articles/kms_list.html) 服务器

```
kms.loli.beer
kms.loli.best
kms.03k.org
kms-default.cangshui.net	
kms.catqu.com
kms.cgtsoft.com
```

设置 [KMS](https://www.coolhub.top/tech-articles/kms_list.html) 服务器

```cmd
C:\Users\sec>slmgr.vbs /skms kms.loli.beer
```

激活

```cmd
C:\Users\sec>slmgr.vbs /ato
```

获取激活状态

```cmd
C:\Users\sec>slmgr.vbs -xpr
```

---

Refrences

- [密钥管理服务 (KMS) 客户端激活和产品密钥](https://learn.microsoft.com/zh-cn/windows-server/get-started/kms-client-activation-keys#windows-server-2008-r2)