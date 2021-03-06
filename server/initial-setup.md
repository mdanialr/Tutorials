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
sudo dnf update
```
# Some Utilities
```
sudo dnf install epel-release -y
sudo dnf install bash-completion vim epel-release unzip wget git htop -y
```
if error install epel-release run:
```
sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
```
or if in Oracle Linux:
```
sudo dnf install oracle-epel-release-el8
```
# Firewall
```
sudo dnf install firewalld
sudo systemctl enable firewalld --now
```
## in /etc/firewalld/firewalld.conf
```
sudo vim /etc/firewalld/firewalld.conf
```
_change this value to no_
> AllowZoneDrifting=no
```
sudo systemctl restart firewalld
```
Allow HTTP & HTTPS (80 & 443)
```
sudo firewall-cmd --permanent --zone=public --add-service=http
sudo firewall-cmd --permanent --zone=public --add-service=https
sudo firewall-cmd --reload
sudo firewall-cmd --zone=public --list-all
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