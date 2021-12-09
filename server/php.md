# Install PHP
_change '__x__' with the desired version e.g. 1 or 0_
```
$ sudo dnf install http://rpms.remirepo.net/enterprise/remi-release-8.rpm -y
$ sudo dnf module enable php:remi-8.x -y
$ sudo dnf install php
```
# Laravel Dependencies
```
$ sudo dnf install php-{fpm,opcache,curl,common,xml,mbstring,json,zip,cli} -y
$ sudo systemctl enable php-fpm --now
```
# Database Driver
> Postgresql
```
$ sudo dnf install php-pgsql -y
```
> Mysql/MariaDB
```
$ sudo dnf install php-mysqlnd  -y
```
# Install Composer
head to <a href="https://getcomposer.org/download/" target="_blank">this</a> link.

verify install with:
```
$ composer
```
## Optional
_to make 'composer' can be executed using sudo_
$ sudo ln -s /usr/local/bin/composer /usr/bin/
$ composer
$ sudo composer