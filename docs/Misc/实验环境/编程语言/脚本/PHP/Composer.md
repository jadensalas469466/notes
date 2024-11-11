## 部署

安装

```shell
┌──(root㉿kali)-[~]
└─# apt install -y composer
```

## 初始化

配置源

```shell
┌──(root㉿kali)-[~]
└─# composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

## 使用

配置源

```shell
┌──(root㉿kali)-[~]
└─# composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

查看 composer 全局配置文件的路径

```shell
┌──(root㉿kali)-[~]
└─# composer global config home
/root/.config/composer
```

查看源

```shell
┌──(root㉿kali)-[~]
└─# composer config --list --global
```

---

参考链接

- [Composer](https://github.com/composer/composer)
