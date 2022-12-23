WordPress
---------

Wordpress is the most popular way to build and host a website. 

Install
--------

    # See Decyphertek - LEMP Stack docs , to prepare the base system. 
    $ sudo mysql
    <OR>
    $ mysql -u root -p
    mysql> CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
    mysql> CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'password';
    mysql> GRANT ALL ON wordpress.* TO 'wordpressuser'@'localhost';
    mysql> exit
    $ sudo apt update && sudo apt install -y php-curl php-gd php-intl php-mbstring php-soap php-xml php-xmlrpc php-zip
    $ sudo systemctl restart php*fpm
    $ sudo vim  /etc/nginx/nginx.conf

    brotli on;
    brotli_comp_level 6;
    brotli_static on;
    brotli_types application/atom+xml application/javascript application/json 
    application/rss+xml
        application/vnd.ms-fontobject application/x-font-opentype application/x-font-
    truetype
        application/x-font-ttf application/x-javascript application/xhtml+xml 
    application/xml
        font/eot font/opentype font/otf font/truetype image/svg+xml 
    image/vnd.microsoft.icon
        image/x-icon image/x-win-bitmap text/css text/javascript text/plain text/xml;
        
    $ sudo vim /etc/nginx/conf.d/custom.conf

    server {
        listen 443 ssl;
        server_name localhost;
        root /var/www/wordpress;
        ssl_certificate      /etc/ssl/certs/self-signed-crt.pem;
        ssl_certificate_key  /etc/ssl/private/self-signed-key.pem;
        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;
        ssl_protocols        TLSV1.1 TLSV1.2 TLSV1.3;
        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers on;
    location / {
        try_files $uri $uri/ /index.php$is_args$args;
        }
    }

    server {
            location = /favicon.ico { log_not_found off; access_log off; }
            location = /robots.txt { log_not_found off; access_log off; allow all; }
            location ~* \.(css|gif|ico|jpeg|jpg|js|png)$ {
                expires max;
                log_not_found off;
            }
    }

    $ sudo nginx -t
    $ cd /tmp
    $ curl -LO https://wordpress.org/latest.tar.gz
    $ tar xzvf latest.tar.gz
    $ cp /tmp/wordpress/wp-config-sample.php /tmp/wordpress/wp-config.php
    $ sudo mkdir /var/www/
    $ sudo cp -a /tmp/wordpress/. /var/www/wordpress
    $ sudo chown -R www-data:www-data /var/www/wordpress
    $ curl -s https://api.wordpress.org/secret-key/1.1/salt/
    # Add generated values
    $ sudo nano /var/www/wordpress/wp-config.php

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