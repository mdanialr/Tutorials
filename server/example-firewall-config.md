## Example Configuration
_open specific port (eg. 8050)_
```
$ sudo firewall-cmd --permanent --zone=public --add-port=8050/tcp
```
_remove specific port (eg. 8050)_
```
$ sudo firewall-cmd --permanent --zone=public --remove-port=8050/tcp
```
_remove service (eg. http, https)_
```
$ sudo firewall-cmd --zone=public --permanent --remove-service=http
$ sudo firewall-cmd --zone=public --permanent --remove-service=https
```
_block specific ip (eg. 3.3.3.3)_
```
$ sudo firewall-cmd --permanent --zone=drop --add-source=3.3.3.3
```