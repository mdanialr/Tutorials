# SSH (as user with sudo privilege)
## in /etc/ssh/sshd_config
```
$ sudo vim /etc/firewalld/firewalld.conf
```
_change these values to no_
> PermitRootLogin no

> PasswordAuthentication no

> X11Forwarding no

```
$ sudo systemctl restart sshd
```