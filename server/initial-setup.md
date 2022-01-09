# Add New User as Admin (as root)
```
# adduser username
# passwd username
# usermod -aG wheel username
```
# SSH
head to <a href="./ssh.md" target="_blank">this</a> link.
# First-time Command
```
$ sudo dnf update
```
# Some Utilities
```
$ sudo dnf install epel-release -y
$ sudo dnf install bash-completion vim epel-release unzip wget git htop -y
```
if error install epel-release run:
```
sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
```
or if in Oracle Linux:
```
sudo tee /etc/yum.repos.d/ol8-epel.repo<<EOF
[ol8_developer_EPEL]
name= Oracle Linux \$releasever EPEL (\$basearch)
baseurl=https://yum.oracle.com/repo/OracleLinux/OL8/developer/EPEL/\$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=1
EOF
```
```
sudo dnf makecache
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
head to <a href="./example-firewall-config.md" target="_blank">this</a> link.
# Install PHP
head to <a href="./php.md" target="_blank">this</a> link.
# Install Database
MariaDB : head to <a href="./mariadb.md" target="_blank">this</a> link.

PostgreSQL : head to <a href="./postgresql.md" target="_blank">this</a> link.
# Install & Config Nginx Web Server
head to <a href="./nginx.md" target="_blank">this</a> link.
# Install & Host Laravel Webapp
head to <a href="./laravel.md" target="_blank">this</a> link.