# SSH (as user with sudo privilege)
- ## in /etc/ssh/sshd_config
```
sudo vim /etc/ssh/sshd_config
```
_change these values to no_
> PermitRootLogin no

> PasswordAuthentication no

> X11Forwarding no

```
sudo systemctl restart sshd
```
- ## in /home/username/
```
mkdir .ssh
```
- ## in /home/username/.ssh
_copy client's .pub file to this directory_