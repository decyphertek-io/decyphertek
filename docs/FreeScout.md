FreeScout
=====

Open Source Zendesk alternative. 

Ubuntu Interactive script
-------------------------

    $ sudo apt install wget 
    $ wget https://raw.githubusercontent.com/freescout-helpdesk/scripts/master/install/ubuntu.sh 
    $ chmod u+x ubuntu.sh 
    $ sudo  bash ubuntu.sh
   
Manual Install
--------------

    $ sudo apt-get update 
    $ sudo apt install nginx 
    $ sudo rm /var/www/html/*nginx*.html
    $ sudo apt install php8.0 php8.0-mysql php8.0-fpm php8.0-mbstring php8.0-xml php8.0-imap php8.0-zip php8.0-gd php8.0-curl
    $ sudo apt install mysql-server libmysqlclient-dev
    $ sudo apt install git
    $ sudo -- "$SHELL" -c "echo 'cgi.fix_pathinfo=0' >> /etc/php/8.0/fpm/php.ini"
    $ mysql -u root -p
    > CREATE USER 'freescout'@'localhost' IDENTIFIED BY 'XXX';
    GRANT ALL PRIVILEGES ON `freescout`.* TO `freescout`@`localhost`;
    > exit
    $ sudo mkdir -p /var/www/html
    $ sudo chown www-data:www-data /var/www/html
    $ cd /var/www/html
    $ wget https://freescout.net/download/
    $ unzip package-name.zip
    $ sudo chown -R www-data:www-data /var/www/html
    $ sudo  usermod -g www-data freescout
    $ find /var/www/html -type f -exec chmod 664 {} \;    
    $ find /var/www/html -type d -exec chmod 775 {} \;
    $ sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/example.com
    $ sudo rm /etc/nginx/sites-enabled/default
    $ sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/example.com
    $ sudo nano /etc/nginx/sites-enabled/example.com
    # config
    server {
        listen 80;
        listen [::]:80;
        server_name example.com www.example.com;
        root /var/www/html/public;
        index index.php index.html index.htm;
        error_log /var/www/html/storage/logs/web-server.log;
        location / {
            try_files $uri $uri/ /index.php?$query_string;
        }
        location ~ \.php$ {
	    fastcgi_split_path_info ^(.+\.php)(/.+)$;
	    fastcgi_pass unix:/run/php/php8.0-fpm.sock;
	    fastcgi_index index.php;
	    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
	    include fastcgi_params;
        }
        # Uncomment this location if you want to improve attachments downloading speed.
        # Also make sure to set APP_DOWNLOAD_ATTACHMENTS_VIA=nginx in the .env file.
        #location ^~ /storage/app/attachment/ {
        #    internal;
        #    alias /var/www/html/storage/app/attachment/;
        }
        location ~* ^/storage/attachment/ {
            expires 1M;
            access_log off;
            try_files $uri $uri/ /index.php?$query_string;
        }
        location ~* ^/(?:css|js)/.*\.(?:css|js)$ {
            expires 2d;
            access_log off;
            add_header Cache-Control "public, must-revalidate";
        }
        location ~* ^/(?:css|fonts|img|installer|js|modules|[^\\\]+\..*)$ {
            expires 1M;
            access_log off;
            add_header Cache-Control "public";
        }
        location ~ /\. {
            deny  all;
        }
    }

    # Apply.config
    $ sudo nginx -t
    $ sudo service nginx reload
    $ sudo snap install --classic certbot
    $ sudo ln -s /snap/bin/certbot /usr/bin/certbot
    $ sudo certbot --nginx
    $ certbot --nginx --register-unsafely-without-email
    $ certbot renew --dry-run
    $ sudo crontab -e
    0 12 * * * /usr/bin/certbot renew --quiet

References
----------

    https://freescout.net/
    https://github.com/freescout-helpdesk/freescout
