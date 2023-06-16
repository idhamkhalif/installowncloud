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

1. Menjalankan MySql:

mysql -u root -p

2. Membuat database :

mysql> CREATE DATABASE owncloud;

mysql> CREATE USER 'owncloud'@'localhost' IDENTIFIED BY 'Str0ngPEd6';

mysql> GRANT ALL PRIVILEGES ON owncloud. * TO 'owncloud'@'localhost';

mysql> FLUSH PRIVILEGES;

mysql> exit;

# 5. Install owncloud

wget https://download.owncloud.com/server/stable/owncloud-complete-latest.zip

unzip owncloud-complete-latest.zip -d /var/www/

mkdir -p /var/www/owncloud/data

chown -R www-data:www-data /var/www/owncloud/

# 6. Konfigurasi Apache untuk owncloud

nano /etc/apache2/sites-available/owncloud.conf

Isi kan script berikut ini :

<VirtualHost *:80>

ServerName cloud.your-domain.com

ServerAdmin webmaster@your-domain.com
DocumentRoot /var/www/owncloud

<Directory /var/www/owncloud/>
Options +FollowSymlinks
AllowOverride All
Require all granted
</Directory>

ErrorLog /var/log/apache2/cloud.your-domain.com_error.log
CustomLog /var/log/apache2/cloud.your-domain.com_access.log combined

</VirtualHost>


