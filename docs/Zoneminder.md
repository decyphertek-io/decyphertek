Zoneminder
==========

"A full-featured, open source, state-of-the-art video surveillance software system."


Prepare System
---------------

    $ sudo apt update
    $ sudo apt-get install tasksel
    $ sudo tasksel install lamp-server
    $ sudo add-apt-repository ppa:iconnor/zoneminder-1.34
    $ sudo apt update && sudo apt upgrade -y

Remove exisitng symbolic link
------------------------------

    $ sudo rm /etc/mysql/my.cnf 
    $ sudo cp /etc/mysql/mysql.conf.d/mysqld.cnf /etc/mysql/my.cnf
    $ sudo vim /etc/mysql/my.cnf
    sql_mode = NO_ENGINE_SUBSTITUTION
    $ sudo systemctl restart mysql

Install Zoneminder
------------------

    $ sudo apt-get install zoneminder

Set Permissions
---------------

    $ sudo chmod 740 /etc/zm/zm.conf 
    $ sudo chown root:www-data 
    $ sudo chown -R www-data:www-data /usr/share/zoneminder/

Configure Apache 
----------------

    $ sudo sudo a2enmod cgi rewrite expires headers
    $ sudo a2enconf zoneminder
    
Edit Timezone
--------------

    > Options > System > Timezone


Firewall
--------

    $ sudo ufw allow in "Apache"
    $ sudo ufw block 80/tcp

Change Default DB
---------

    Changed Default DB User: If you have changed your DB login/password from zmuser/zmpass, 
    you need to update these values in zm.conf. Edit zm.conf to change ZM_DB_USER and ZM_DB_PASS 
    to the values you used.

Enable User Authentication
--------------------------

    Login to Zoneminder > Options > System >
    OPT_USE_AUTH = Enable
    AUTH_TYPE = Built In
    AUTH_RELAY = Hashed
    AUTH_HASH_SECRET = generate via - $ openssl passwd -6  ( Paste hash into box)
    AUTH_HASH_IP = disabled
    AUTH_HASH_LOGINS = Enabled

    http://ip-of-server/zm
    user: admin
    pass: admin

    # Change password
    Login > options > system > user > make a new user with same privileges or change password on admin


Enable SSL
----------

    $ sudo a2enmod ssl
    $ sudo systemctl restart apache2
    $ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache.key -out /etc/ssl/certs/apache.crt
    $ sudo vim /etc/apache2/sites-available/default-ssl.conf

    <VirtualHost *:443>
    ServerName 127.0.0.1
    DocumentRoot /usr/share/zoneminder/www
    
    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/apache.crt
    SSLCertificateKeyFile /etc/ssl/private/apache.key
    </VirtualHost>

    $ sudo vim /etc/apache2/sites-available/000-default.conf
    <VirtualHost *:80>
	ServerName 127.0.0.1
    DocumentRoot /usr/share/zoneminder/www
	Redirect / https://127.0.0.1/zm
    </VirtualHost>

    $ sudo a2ensite default-ssl.conf
    $ sudo systemctl reload apache2
   
Manage Zoneminder & Apache
-------------------------

    $ sudo systemctl enable zoneminder
    $ sudo systemctl start zoneminder
    $ sudo systemctl reload apache2
    $ sudo systemctl restart apache2

TroubleShoot
-------------

    $ sudo apache2ctl configtest
    $ sudo systemctl status apache2.service -l --no-pager
    $ sudo journalctl -u apache2.service --since today --no-pager

Login
-----

    http://hostname_or_ip/zm

Api 
---

    http://hostname_or_ip/zm/api/host/getVersion.json

References
----------

    https://zoneminder.readthedocs.io/en/stable/installationguide/ubuntu.html
    https://www.howtogeek.com/devops/how-to-create-and-use-self-signed-ssl-on-apache/
    https://www.how2shout.com/linux/how-to-install-zoneminder-on-ubuntu-22-04-20-04-lts/