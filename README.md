# Install Owncloud Ubuntu

# 1. Install Apache2 HTTP Server

sudo apt install apache2

sudo sed -i "s/Options Indexes FollowSymLinks/Options FollowSymLinks/" /etc/apache2/apache2.conf

sudo systemctl stop apache2.service

sudo systemctl start apache2.service

sudo systemctl enable apache2.service

# 2. Install PHP and Related Modules

sudo apt-get install software-properties-common -y

sudo add-apt-repository ppa:ondrej/php

sudo apt update

sudo apt install php7.1 libapache2-mod-php7.1 php7.1-common php7.1-mbstring php7.1-xmlrpc php7.1-soap php7.1-apcu php7.1-smbclient php7.1-ldap php7.1-redis php7.1-gd php7.1-xml php7.1-intl php7.1-json php7.1-imagick php7.1-mysql php7.1-cli php7.1-mcrypt php7.1-ldap php7.1-zip php7.1-curl -y

sudo nano /etc/php/7.1/apache2/php.ini

Ganti Settingan sesuai berikut :
file_uploads = On
allow_url_fopen = On
memory_limit = 256M
upload_max_filesize = 100M
display_errors = Off
date.timezone = America/Florida

# 3.Membuat Owncloud Database

sudo mysql -u root -p

CREATE DATABASE owncloud;

CREATE USER 'ownclouduser'@'localhost' IDENTIFIED BY 'password_here';

GRANT ALL ON owncloud.* TO 'ownclouduser'@'localhost' IDENTIFIED BY 'password_here' WITH GRANT OPTION;

FLUSH PRIVILEGES;

EXIT;

# 4. Download Latest OwnCloud Release

cd /tmp && wget https://download.owncloud.org/community/owncloud-10.0.8.zip

unzip owncloud-10.0.8.zip

sudo mv owncloud /var/www/html/owncloud/

sudo chown -R www-data:www-data /var/www/html/owncloud/

sudo chmod -R 755 /var/www/html/owncloud/

# 5. Configure Apache2

sudo nano /etc/apache2/sites-available/owncloud.conf

Copy dan paste code berikut ini :
<VirtualHost *:80>
     ServerAdmin admin@example.com
     DocumentRoot /var/www/html/owncloud/
     ServerName avoiderrors.com
     ServerAlias www.avoiderrors.com
  
     Alias /owncloud "/var/www/html/owncloud/"

     <Directory /var/www/html/owncloud/>
        Options +FollowSymlinks
        AllowOverride All
        Require all granted
          <IfModule mod_dav.c>
            Dav off
          </IfModule>
        SetEnv HOME /var/www/html/owncloud
        SetEnv HTTP_HOME /var/www/html/owncloud
     </Directory>

     ErrorLog ${APACHE_LOG_DIR}/error.log
     CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>

# 6. Enable the OwnCloud and Rewrite Module

sudo a2ensite owncloud.conf
sudo a2enmod rewrite
sudo a2enmod headers
sudo a2enmod env
sudo a2enmod dir
sudo a2enmod mime

sudo systemctl restart apache2.service


