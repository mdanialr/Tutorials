# Install MariaDB
_change '__x__' to the desired version e.g. 3 or 5_
```
$ sudo dnf module list mariadb
$ sudo dnf module enable mariadb:10.x -y
$ sudo dnf install mariadb-server -y
$ sudo mariadb-secure-installation
$ sudo systemctl enable mariadb --now
$ sudo systemctl status mariadb
```
# Create New DB & User
```
$ sudo mariadb -u root -p
```
## in MariaDB Console
> **Notes**: if you need user can be accessed by another host other than this machine or you need to access this database from another network, **change** _'localhost'_ to _'%'_ to accept connection from all network so it can be accessed.
```
MariaDB [(none)]> use mysql;
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
$ sudo mariadb-dump --opt -u username -p database-name > backup-file-name
$ sudo mariadb -u root -p database-name < backup-file-name
```