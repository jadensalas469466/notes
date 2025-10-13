rsync is an open source utility that provides fast incremental file transfer.

## 1. Install

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y rsync
```

## 2. Init

将共享文件夹挂载到本地

```
┌──(nemo@debian)-[~]
└─$ sudo mount -t cifs //192.168.0.57/D /home/nemo/smb -o username=share
```

同步到文档目录

```
┌──(nemo@debian)-[~]
└─$ rsync -av --delete ~/smb/backup/* ~/Documents/
```

取消挂载

```
┌──(nemo@debian)-[~]
└─$ sudo umount /home/nemo/smb
```

## 3. Usage

增量同步, 将 a 目录本身同步到 b 目录

```
┌──(nemo@debian)-[~]
└─$ sudo rsync -av --delete ~/a ~/b
```

增量同步, 将 a 目录的内容同步到 b 目录

```
┌──(nemo@debian)-[~]
└─$ sudo rsync -av --delete ~/a/* ~/b/
```

模拟增量同步, 将 a 目录本身同步到 b 目录

```
┌──(nemo@debian)-[~]
└─$ sudo rsync -av --delete --dry-run ~/a ~/b
```

模拟增量同步, 将 a 目录的内容同步到 b 目录

```
┌──(nemo@debian)-[~]
└─$ sudo rsync -av --delete --dry-run ~/a/* ~/b/
```

---

References

- [rsync](https://rsync.samba.org/)