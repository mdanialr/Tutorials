# Install Nginx
```
sudo dnf install nginx -y
sudo systemctl enable nginx --now
sudo systemctl status nginx
```
# Config Reverse Proxy
## PHP Reverse Proxy: php-fpm
- ### in /etc/php-fpm.d/www.conf
```
sudo vim /etc/php-fpm.d/www.conf
```
_change to these values_
> user = nginx

> group = nginx

> listen.owner = nginx

> listen.group = nginx

> listen.mode = 0666

> listen.acl_users = apache,nginx

> security.limit_extensions = .php .php3 .php4 .php5 .php7

- ### in /etc/php.ini
```
sudo vim /etc/php.ini
```
_change to these values_
> date.timezone = Asia/Jakarta

> cgi.fix_pathinfo=0
```
sudo systemctl restart php-fpm
```

# Increase Max Upload Size
Use the http, server, or location block to edit client_max_body_size:
```nginx
http {
    ...
    client_max_body_size 50M;
}

server {
    ...
    client_max_body_size 50M;
}

location /uploads {
    ...
    client_max_body_size 50M;
}
```
Edit the file in `/etc/nginx/nginx.conf` to set the default size for all vHost then set in `server` block to set the more specific size.