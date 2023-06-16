# Install Owncloud

# 1. Update operating system
apt update && sudo apt upgrade -y

# 2.  Install Apache webserver
apt install apache2

systemctl start apache2
systemctl enable apache2

systemctl status apache2
# output
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: active (running)
       Docs: https://httpd.apache.org/docs/2.4/
    Process: 845 ExecStart=/usr/sbin/apachectl start (code=exited, status=0/SUCCESS)
   Main PID: 998 (apache2)
      Tasks: 6 (limit: 2797)
     Memory: 27.4M
        CPU: 420ms
     CGroup: /system.slice/apache2.service
             ├─ 998 /usr/sbin/apache2 -k start
             ├─1033 /usr/sbin/apache2 -k start
             ├─1034 /usr/sbin/apache2 -k start
             ├─1035 /usr/sbin/apache2 -k start
             ├─1037 /usr/sbin/apache2 -k start
             └─1038 /usr/sbin/apache2 -k start
