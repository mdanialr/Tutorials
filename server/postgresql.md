# Install Repository RPM:
```
$ sudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-8-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
# Install PostgreSQL:
_change '__x__' to the desired version e.g. 13 or 14_
```
$ sudo dnf module list postgresql
$ sudo dnf module enable postgresql:x -y
$ sudo dnf install postgresql-server -y
```
# Post-installation
> Due to policies for Red Hat family distributions, the PostgreSQL installation will not be enabled for automatic start or have the database initialized automatically. To make your database installation complete, you need to perform the following steps, based on your distribution: 
```
$ sudo postgresql-setup --initdb
$ sudo systemctl enable postgresql.service
```
> **Note**: if there is error not empty use '$ sudo rm -rf /var/lib/pgsql/data'
## Allow DB Connection from php-fpm in SELinux
```
$ sudo setsebool -P httpd_can_network_connect_db 1
$ sudo systemctl restart postgresql
```
## in /var/lib/pgsql/data/pg_hba.conf
```
$ sudo vim /var/lib/pgsql/data/pg_hba.conf
```
_use md5 password instead ident_
> host all all 127.0.0.1/32 md5
```
$ sudo systemctl restart postgresql
```
# Create New DB & Role
```
$ sudo -u postgres psql
```
## in PostgreSQL Console
> **Note**: if you need user can be accessed by another host other than this machine or you need to access this database from another network, **change** _'localhost'_ to _'%'_ to accept connection from all network so it can be accessed.
```
postgres=# CREATE DATABASE dbname OWNER username;
postgres=# CREATE ROLE username WITH LOGIN ENCRYPTED PASSWORD 'thepassword';
postgres=# \c dbname;
dbname=# GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO username;
dbname=# GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA public TO username;
```
> **Note**: FLUSH PRIVILEGES ? of course **not** needed it is **Postgre** after all.
# Backup & Restore (logical)
## All Databases
- Backup
```
$ sudo -u postgres pg_dumpall --clean --no-owner > dumpfilename
```
- Restore
```
$ sudo -u postgres psql postgres < dumpfilename
```
## Exclude Some Databases
- Backup

_change **db1** & **db3** to the desired database_
```
$ sudo -u postgres pg_dumpall --clean --no-owner --exclude-database=db1 --exclude-database=db3 > dumpfilename
```
- Restore
```
$ sudo -u postgres psql postgres < dumpfilename
```
> **Note**: you can add _--exclude-database=dbname_ as many as you needed
# Only One Database
- Backup
```
$ sudo -u postgres pg_dump dbname > dumpfilename
```
- Restore
```
$ sudo -u postgres psql -d newdbname -f dumpfilename
```