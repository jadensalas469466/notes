Damn Vulnerable Web Application (DVWA).

## 1. Install

安装依赖

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y apache2 mariadb-server mariadb-client php php-mysql php-gd libapache2-mod-php composer
```

Enable

```
┌──(nemo@debian)-[~]
└─$ sudo systemctl enable --now mysql.service \
&& sudo systemctl enable --now apache2.service \
&& sudo a2enmod rewrite \
&& sudo systemctl restart apache2.service
```

Clone

```
┌──(nemo@debian)-[~]
└─$ sudo -E git clone https://github.com/digininja/DVWA.git /var/www/html/dvwa
```

Install API module

```
┌──(nemo@debian)-[~]
└─$ sudo composer install -d /var/www/html/dvwa/vulnerabilities/api
```

## 2. Init

端口转发

```
/Machines/VM/Settings/Expert/Network/Adapter 1/Port Forwarding
```

| Name | Host Port | Guest Port |
| -------- | ------------- | --------------- |
| Web    | 60080      | 80              |

配置数据库密码

```
┌──(nemo@debian)-[~]
└─$ sudo mysql -u root -p
```

```
Enter password:
```

```
MariaDB [(none)]> ALTER USER root@localhost IDENTIFIED BY '123456';
FLUSH PRIVILEGES;
EXIT;
```

Folder Permissions

```
┌──(nemo@debian)-[~]
└─$ sudo chown -R www-data:www-data /var/www/html/dvwa/hackable/uploads /var/www/html/dvwa/config \
&& sudo chmod -R 775 /var/www/html/dvwa/hackable/uploads /var/www/html/dvwa/config
```

PHP Configuration

```
┌──(nemo@debian)-[~]
└─$ sudo cp /etc/php/8.2/apache2/php.ini /etc/php/8.2/apache2/php.ini.bak \
&& sudo nano -l /etc/php/8.2/apache2/php.ini \
&& sudo systemctl restart apache2.service
```

```
508 display_errors = On
517 display_startup_errors = On
866 allow_url_fopen = On
870 allow_url_include = On
```

DVWA Configuration

```
┌──(nemo@debian)-[~]
└─$ sudo cp /var/www/html/dvwa/config/config.inc.php.dist /var/www/html/dvwa/config/config.inc.php \
&& sudo nano -l /var/www/html/dvwa/config/config.inc.php
```

```
20 $_DVWA[ 'db_user' ]     = getenv('DB_USER') ?: 'root';
21 $_DVWA[ 'db_password' ] = getenv('DB_PASSWORD') ?: '123456';
27 $_DVWA[ 'recaptcha_public_key' ]  = '6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ_MXjiZKhI';
28 $_DVWA[ 'recaptcha_private_key' ] = '6LeIxAcTAAAAAGG-vFI1TnRWxMZNFuojJ4WifJWe';
33 $_DVWA[ 'default_security_level' ] = getenv('DEFAULT_SECURITY_LEVEL') ?: 'low';
```

Click `Create / Reset Database` 

> http://127.0.0.1:60080/dvwa/setup.php

## 3. Usage

Login `admin:password` 

> http://127.0.0.1:60080/dvwa/login.php

---

References

- [DVWA](https://github.com/digininja/DVWA)

