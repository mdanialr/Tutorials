# Install PHPMyAdmin with Nginx on RockyLinux 8 / RHEL 8
### **Note**: Make sure php-fpm already installed.
- install in `/opt/`
```
$ cd /opt
$ sudo composer create-project phpmyadmin/phpmyadmin phpmyadmin
$ cd phpmyadmin
$ sudo composer update # optional
```
- permissions
```
$ cd /opt
$ sudo chown :nginx -R phpmyadmin
$ sudo chown :nginx -R /var/lib/php/session
```
- copy config file
```
$ cd /opt/phpmyadmin
$ sudo cp config.sample.inc.php config.inc.php
```
- generate blowfish value. eg. from [here](https://phpsolved.com/phpmyadmin-blowfish-secret-generator/).
- open up config.inc.php
```
$ sudo vim config.inc.php
```
- change to these values
> $cfg['blowfish_secret'] = 'paste-generated-blowfish-value-here';

> $cfg['TempDir'] = '/tmp';

- Nginx vHost
```
server {
	listen   80;
	server_name php.admin;
	root /opt/phpmyadmin;

	location / {
		index  index.php;
	}

	## Images and static content is treated different
	location ~* ^.+.(jpg|jpeg|gif|css|png|js|ico|xml)$ {
		access_log        off;
		expires           30d;
	}

	location ~ /\.ht {
		deny  all;
	}

	location ~ /(libraries|setup/frames|setup/libs) {
		deny all;
		return 404;
	}

	location ~ \.php$ {
		include fastcgi_params;
		fastcgi_pass unix:/run/php-fpm/www.sock;
		fastcgi_param SCRIPT_FILENAME /opt/phpmyadmin$fastcgi_script_name;
	}
}
```
- add custom host `php.admin` in /etc/hosts
```
127.0.0.1 .... php.admin
```