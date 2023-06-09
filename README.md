# Install Owncloud Ubuntu

#1.Install Apache2 HTTP Server

sudo apt install apache2

sudo sed -i "s/Options Indexes FollowSymLinks/Options FollowSymLinks/" /etc/apache2/apache2.conf

sudo systemctl stop apache2.service

sudo systemctl start apache2.service

sudo systemctl enable apache2.service


