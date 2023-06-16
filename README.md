# Install Owncloud

# 1. Update operating system
apt update && sudo apt upgrade -y

# 2.  Install Apache webserver
apt install apache2

systemctl start apache2
systemctl enable apache2

systemctl status apache2

# 3. Install PHP dan Extentionnya
add-apt-repository ppa:ondrej/php

apt update

apt install php7.4 php7.4-{opcache,gd,curl,mysqlnd,intl,json,ldap,mbstring,mysqlnd,xml,zip}

# 4. Install MySql untuk database dan membuat database

apt install mysql-server

systemctl start mysql
systemctl enable mysql

systemctl status mysql

Konfigurasi MySql :
mysql_secure_installation

- Set root password? [Y/n] Y
- Remove anonymous users? [Y/n] Y
- Disallow root login remotely? [Y/n] Y
- Remove test database and access to it? [Y/n] Y
- Reload privilege tables now? [Y/n] Y

mysql -u root -p

Membuat database :
mysql> CREATE DATABASE owncloud;
mysql> CREATE USER 'owncloud'@'localhost' IDENTIFIED BY 'Str0ngPEd6';


