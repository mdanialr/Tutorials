# Add New User as Admin (as root)
```
# adduser username
# passwd username
# usermod -aG wheel username
```
# SSH
head to [this](/server/ssh.md) link.
# First-time Command
```
$ sudo dnf update
```
# Some Utilities
```
$ sudo dnf install bash-completion vim epel-release unzip wget git htop -y
```
# Firewall
```
$ sudo dnf install firewalld
$ sudo systemctl enable firewalld --now
```
## in /etc/firewalld/firewalld.conf
```
$ sudo vim /etc/firewalld/firewalld.conf
```
_change this value to no_
> AllowZoneDrifting=no
```
$ sudo systemctl restart firewalld
```
```
$ sudo firewall-cmd --permanent --zone=public --add-service=http
$ sudo firewall-cmd --permanent --zone=public --add-service=https
$ sudo firewall-cmd --reload
$ sudo firewall-cmd --zone=public --list-all
```
## Example Configuration
head to [this](/server/example-firewall-config.md) link.

