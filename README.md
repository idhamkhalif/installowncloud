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


