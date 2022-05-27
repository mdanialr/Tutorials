# Install MariaDB
_change '__x__' to the desired version e.g. 3 or 5_
```
sudo dnf module list mariadb
sudo dnf module enable mariadb:10.x -y
sudo dnf install mariadb-server -y
sudo systemctl enable mariadb --now
sudo systemctl status mariadb
sudo mariadb-secure-installation
```
## Allow DB Connection from php-fpm in SELinux
```
sudo setsebool -P httpd_can_network_connect_db 1
```
# Create New DB & User
```
sudo mariadb -u root -p
```
_in MariaDB Console_
> **Notes**: if you need user can be accessed by another host other than this machine or you need to access this database from another network, **change** _'localhost'_ to _'%'_ to accept connection from all network so it can be accessed.
```
MariaDB [(none)]> use mysql;
MariaDB [mysql]> CREATE DATABASE DATABASE_NAME;
MariaDB [mysql]> CREATE USER 'USER_NAME'@'localhost' IDENTIFIED BY 'PASSWORD';
MariaDB [mysql]> GRANT ALL PRIVILEGES ON DATABASE_NAME.* TO 'USER_NAME'@'localhost';
MariaDB [mysql]> SHOW GRANTS FOR 'USER_NAME'@'localhost';
MariaDB [mysql]> FLUSH PRIVILEGES;
```
> If you are in older Mysql or MariaDB then use this for granting privileges instead    
```
mysql> GRANT ALL PRIVILEGES ON DATABASE_NAME.* TO 'USER_NAME'@'localhost' IDENTIFIED BY 'PASSWORD';
```
# Backup & Restore (logical)
```
sudo mariadb-dump --opt -u username -p database-name > backup-file-name
sudo mariadb -u root -p database-name < backup-file-name
```
## in Docker Container
```bash
# Backup
docker exec -t container_name mariadb-dump --opt -u root -p[password] database-name > backup-file-name
# Restore
docker exec -i container_name mariadb -u root -p[password] database-name < backup-file-name
```
# Reset Password User **root**
```
sudo systemctl stop mariadb
sudo mariadbd --skip-grant-tables --user=mysql &
```
_in new terminal_
```
sudo mariadb -u root
```
_then in MariaDB Console_
```
MariaDB [(none)]> use mysql;
MariaDB [mysql]> ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_passowrd';
```
> **Note**: if there is error password not meet requirements, then set requirements to LOW:
```
MariaDB [mysql]> SHOW VARIABLES LIKE 'validate_password%';
MariaDB [mysql]> SET GLOBAL validate_password_policy=LOW;
## then try to change the password again
MariaDB [mysql]> ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_passowrd';
```
then reboot the machine
```
sudo reboot
```