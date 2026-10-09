LEMP Stack
==========

LEMP stands for Linux, Nginx ( Engine-X ), MySQL, and PHP. This guide goes a step
further and adds phpMyAdmin and PHP Composer. For Nginx with Modsecurity WAF,
see the Decyphertek Nginx docs.

System Update
-------------
```
sudo apt update && sudo apt upgrade
```

Nginx
-----
* See the Decyphertek Nginx docs for how to install Nginx with the Modsecurity WAF.

MySQL
-----
* See the Decyphertek MySQL docs for day-to-day management. The commands below
  cover the initial install and passwords.
```
sudo apt install mysql-server
```
* Set a root MySQL password:
```
sudo mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
exit
```
* Debian generates a non-secure password for the debian-sys-maint user, stored in
  /etc/mysql/debian.cnf. View it:
```
sudo cat /etc/mysql/debian.cnf
```
* Set a new debian-sys-maint password and update /etc/mysql/debian.cnf to match:
```
sudo mysqladmin -u debian-sys-maint -p'oldPassword' password 'newPassword'
sudo vim /etc/mysql/debian.cnf
sudo mysql_secure_installation
```
* Verify both logins work:
```
mysql -u root -p
exit
mysql -u debian-sys-maint -p
exit
```

PHP
---
```
sudo apt install php-mysql php-fpm php-curl php-gd php-mbstring php-xml php-xmlrpc php-cli
```

phpMyAdmin ( Optional )
-----------------------
* Caution: phpMyAdmin requires additional setup to secure and get working with
  Nginx - see the Digital Ocean reference below before exposing it.
```
sudo apt-get -y install apt-transport-https ca-certificates curl
curl -fsSL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x42636ff8dae547240e01a1ca2ea3055293cb3f45" | sudo gpg --dearmor -o /usr/share/keyrings/phpmyadmin-ppa.gpg
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/phpmyadmin-ppa.gpg] https://ppa.launchpadcontent.net/phpmyadmin/ppa/ubuntu jammy main" > /etc/apt/sources.list.d/phpmyadmin-ubuntu-ppa-jammy.list'
sudo apt update
sudo apt install -y phpmyadmin
```

PHP Composer
------------
```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
sudo mv composer.phar /usr/local/bin/composer
```
* Verify and update:
```
composer list
composer self-update
```

References
----------

    https://www.linode.com/docs/guides/how-to-install-a-lemp-stack-on-ubuntu-22-04/
    https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-22-04
    https://www.linode.com/docs/guides/installing-and-using-php-composer/
    https://github.com/phpmyadmin/phpmyadmin/wiki/DebianUbuntu
    https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-with-nginx-on-an-ubuntu-20-04-server
