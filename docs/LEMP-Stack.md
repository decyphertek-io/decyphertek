LEMP Stack
==========

LEMP Stack stands for Linux , Nginx , Mysql, and Php. The instructions here go further
and add myphpadmin, composer and on the nginx docs page , modsecuirty waf. 

Install
-------

    $ sudo apt update && sudo apt upgrade
    # See Decyphertek - nginx docs how how to install nginx with modsecurity waf. 
    # Install mysql - See Decyphertek - mysql docs on how to manage mysql 
    $ sudo apt install mysql-server
    $ sudo mysql_secure_installation
    $ sudo mysql
    mysql>  exit
    # Install PHP
    $ sudo apt install php-mysql php-fpm php-curl php-gd php-mbstring php-xml php-xmlrpc php-cli
    # Install myphpadmin
    $ sudo apt-get -y install apt-transport-https ca-certificates curl
    $ curl -fsSL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x42636ff8dae547240e01a1ca2ea3055293cb3f45" | sudo gpg --dearmor -o /usr/share/keyrings/phpmyadmin-ppa.gpg
    $ sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/phpmyadmin-ppa.gpg] https://ppa.launchpadcontent.net/phpmyadmin/ppa/ubuntu jammy main" > /etc/apt/sources.list.d/phpmyadmin-ubuntu-ppa-jammy.list'
    $ sudo apt update
    $ sudo apt install phpmyadmin
    # install PHP Composer 
    $  php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
    $ php -r "if (hash_file('sha384', 'composer-setup.php') === 'installer-checksum') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
    $  php composer-setup.php
    $ php -r "unlink('composer-setup.php');"
    $ sudo mv composer.phar /usr/local/bin/composer
    $ php composer.phar
    $ composer
    # Update Composer
    $ composer -V
    $ composer self-update

References
----------

    https://www.linode.com/docs/guides/how-to-install-a-lemp-stack-on-ubuntu-22-04/
    https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-22-04
    https://www.linode.com/docs/guides/installing-and-using-php-composer/
    https://github.com/phpmyadmin/phpmyadmin/wiki/DebianUbuntu