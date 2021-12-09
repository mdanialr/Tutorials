# Setup Laravel

## Script
Save scripts below, then run it.
### SELinux Setup
```
#!/usr/bin/bash
set -e

read -p "Root dir: " rootdir
cd $rootdir

sudo chown -R :nginx storage && sudo chown -R :nginx bootstrap/cache && sudo chmod -R 0775 storage && sudo chmod -R 0775 bootstrap/cache

sudo semanage fcontext -at httpd_sys_rw_content_t "$rootdir/storage(/.*)?"
sudo semanage fcontext -at httpd_sys_rw_content_t "$rootdir/bootstrap/cache(/.*)?"
sudo restorecon -R "$rootdir/"
```
### Nginx vHost Setup
```
#!/usr/bin/bash
set -e

read -p "Domain: " domain
read -p "Root dir: " rootdir
read -p "vHost name: " vhost

sudo cat > "/etc/nginx/conf.d/$vhost.conf" <<EOF
server {
    listen 80;
    server_name $domain;
    root $rootdir/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";

    index index.php;

    charset utf-8;

    location / {
        try_files \$uri \$uri/ /index.php?\$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/run/php-fpm/www.sock;
        fastcgi_param SCRIPT_FILENAME \$realpath_root\$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
EOF

sudo nginx -t
sudo systemctl reload nginx
```
## How to Use Script (example)
### Save both scripts in `home/scripts` directory.
```
$ sudo vim /home/username/scripts/selinux-laravel
```
- then copy paste the `SELinux Setup` script and save  it.
```
$ sudo vim /home/username/scripts/vhost-nginx-laravel
```
- then copy paste the `Nginx vHost Setup` script and save  it.

### Run the script.
```
$ cd /home/username/scripts
$ sudo ./selinux-laravel
```
- Fill in 'Root dir:' with where the laravel root project exist. e.g. `/var/www/example-project`. **Note**: without trailing slash.
```
$ cd /home/username/scripts
$ sudo ./vhost-nginx-laravel
```
- Fill in **'Domain:'** with the desired domain. e.g. `example.com`, `example.net`, or `localhost`.
- Fill in **'Root dir:'** with where the laravel root project exist. e.g. `/var/www/example-project`. **Note**: without trailing slash.
- Fill in **'vHost name:'** with the desired filename for this vHost in nginx directory (`/etc/nginx/conf.d/`).