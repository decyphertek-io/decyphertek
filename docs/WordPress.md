WordPress
---------

Wordpress is the most popular way to build and host a website. 

Install
--------

    # See Decyphertek - LEMP Stack docs , to prepare the base system. 
    $ sudo mysql
    mysql> CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
    mysql> CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'password';
    mysql> GRANT ALL ON wordpress.* TO 'wordpressuser'@'localhost';
    mysql> exit
    $ sudo apt update 
    $ sudo apt install php-curl php-gd php-intl php-mbstring php-soap php-xml php-xmlrpc php-zip
    $ sudo systemctl restart php*fpm
    $ sudo nano /etc/nginx/sites-available/wordpress

    server {
        . . .

        location = /favicon.ico { log_not_found off; access_log off; }
        location = /robots.txt { log_not_found off; access_log off; allow all; }
        location ~* \.(css|gif|ico|jpeg|jpg|js|png)$ {
            expires max;
            log_not_found off;
        }
        . . .
}
    $ sudo nano /etc/nginx/sites-available/wordpress
    
    server {
        . . .
        location / {
            #try_files $uri $uri/ =404;
            try_files $uri $uri/ /index.php$is_args$args;
        }
        . . .
    }

    $ sudo nginx -t
    $ cd /tmp
    $ curl -LO https://wordpress.org/latest.tar.gz
    $ tar xzvf latest.tar.gz
    $ cp /tmp/wordpress/wp-config-sample.php /tmp/wordpress/wp-config.php
    $ sudo cp -a /tmp/wordpress/. /var/www/wordpress
    $ sudo chown -R www-data:www-data /var/www/wordpress
    $ curl -s https://api.wordpress.org/secret-key/1.1/salt/
    # Add generated values
    $ sudo nan /var/www/wordpress/wp-config.php

    . . .
    define('AUTH_KEY',         'put your unique phrase here');
    define('SECURE_AUTH_KEY',  'put your unique phrase here');
    define('LOGGED_IN_KEY',    'put your unique phrase here');
    define('NONCE_KEY',        'put your unique phrase here');
    define('AUTH_SALT',        'put your unique phrase here');
    define('SECURE_AUTH_SALT', 'put your unique phrase here');
    define('LOGGED_IN_SALT',   'put your unique phrase here');
    define('NONCE_SALT',       'put your unique phrase here');
    . . .
    define( 'DB_NAME', 'wordpress' );

    /** MySQL database username */
    define( 'DB_USER', 'wordpressuser' );

    /** MySQL database password */
    define( 'DB_PASSWORD', 'password' );
    . . .
    define( 'FS_METHOD', 'direct' );

    # Go to new webpage and setup. 
    http://server_domain_or_IP/wordpress

References
----------

    https://wordpress.org/download/
    https://wordpress.org/support/article/how-to-install-wordpress/
    https://www.linode.com/docs/guides/how-to-install-a-lemp-stack-on-ubuntu-22-04/
    https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-with-lemp-on-ubuntu-20-04