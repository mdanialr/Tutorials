# Install Nginx
```
$ sudo dnf install nginx -y
$ sudo systemctl enable nginx --now
$ sudo systemctl status nginx
```
# Config Reverse Proxy
## PHP Reverse Proxy: php-fpm
- ### in /etc/php-fpm.d/www.conf
```
$ sudo vim /etc/php-fpm.d/www.conf
```
_change to these values_
> user = nginx

> group = nginx

> listen.owner = nginx

> listen.group = nginx

> listen.mode = 0666

> security.limit_extensions = .php .php3 .php4 .php5 .php7

- ### in /etc/php.ini
```
$ sudo vim /etc/php.ini
```
_change to these values_
> date.timezone = Asia/Jakarta

> cgi.fix_pathinfo=0
```
$ sudo systemctl restart php-fpm
```