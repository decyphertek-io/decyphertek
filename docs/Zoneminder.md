Zoneminder
==========

"A full-featured, open source, state-of-the-art video surveillance software system."


Version
-------

    V1.34.26
    Ubuntu 20.04 LTS 

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


Enable User Authentication
--------------------------

    Login > Options > System >
    OPT_USE_AUTH = Enable
    AUTH_TYPE = Built In
    AUTH_RELAY = Hashed
    AUTH_HASH_SECRET = generate via command: $ openssl passwd -6  ( and Paste hash into box)
    AUTH_HASH_IP = disabled
    AUTH_HASH_LOGINS = Enabled
    save

    http://ip-of-server/zm
    user: admin
    pass: admin

    # Change password
    Login > options > system > user > make a new user with same privileges or change password on admin


Enable SSL
----------
    
    Note:
    There is a glitch in the way that Zoneminder uses Apache. Redirects to /zm do not appear to work.
    Once you have SSL set, have to manually go to https://ip-of-server/zm . Using the zoneminder directory
    /usr/share/zonmeinder/www has permission issues. Solving the redirect or the permisison issues appears
    to be a solution. A simple solution is to make an index.html page that states to go to /zm to login. 

    $ sudo a2enmod ssl
    $ sudo systemctl restart apache2
    $ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache.key -out /etc/ssl/certs/apache.crt
    $ sudo vim /etc/apache2/sites-available/default-ssl.conf

    <VirtualHost *:443>
    ServerName 127.0.0.1
    DocumentRoot /var/www/html
    #Redirect "/" "https://${APACHE_IP}/zm"
    
    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/apache.crt
    SSLCertificateKeyFile /etc/ssl/private/apache.key
    </VirtualHost>

    $ sudo vim /etc/apache2/envars
    export APACHE_IP=$(dig +short myip.opendns.com @resolver1.opendns.com)

    $ sudo vim /etc/apache2/sites-available/000-default.conf
    <VirtualHost *:80>
	ServerName 127.0.0.1
    DocumentRoot /var/www/html
	Redirect / https://${APACHE_IP}/
    </VirtualHost>

    $ sudo a2ensite default-ssl.conf
    $ sudo systemctl reload apache2

Email SSMTP
-----------

    $ sudo apt update
    $ sudo apt install ssmtp mailutils
    $ sudo vim /etc/ssmtp/ssmtp.conf
    
    # MailGun Example:
    root=postmaster@domain.com
    mailhub=smtp.mailgun.org:587
    rewriteDomain=domain.com
    hostname=localhost
    UseTLS=Yes
    UseSTARTTLS=Yes
    AuthUser=email
    AuthPass=password

    # GMail Example
    root=example@gmail.com
    mailhub=smtp.gmail.com:587
    hostname=localhost
    RewriteDomain=gmail.com
    UseSTARTTLS=YES
    UseTLS=YES
    AuthUser=example@gmail.com
    AuthPass=password

    $ sudo vim /etc/ssmtp/revaliases
    root:example@gmail.com:smtp.gmail.com:587
    www-data:example@gmail.com:smtp.gmail.com:587

    # Login to Zoneminder
    > Options > Email :
    EMAIL_HOST = locallhost
    FROM_EMAIL = zoneminder@domain.com
    SSMTP_MAIL = enabled
    SSMTP_PATH = /usr/sbin/ssmtp

    # Test
    $ vim test.txt
    write something here to test. 
    $ ssmtp -v ExampleTest@gmail.com < test.txt
    <OR>
    $ echo "Your Email Body" | mail -s "your subject" ExamplTest@gmail.com

Zoneminder App
--------------
    # zmNinja-pro
    https://zmninja.zoneminder.com/
    # Use zm authetnication
    # enter username & password. 
    # Get an error - cgi-bin detection failed-No configureg/enabled monitor Zoneminder
    # continue past error, should see the server from your phone.

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
    # There is a redirect bug, need to have the /zm added . 
    https://hostname_or_ip/zm

Api 
---

    http://hostname_or_ip/zm/api/host/getVersion.json


Optional: Change Default DB
----------------------------

    Note:
    Changed Default DB User: If you have changed your DB login/password from zmuser/zmpass, 
    you need to update these values in zm.conf. Edit zm.conf to change ZM_DB_USER and ZM_DB_PASS 
    to the values you used. 

    # Set root password
    $ sudo mysql
    mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
    mysql> FLUSH PRIVILEGES;
    mysql> exit

    # The root password has been set by you from the above command, optional to change. 
    $ sudo mysqladmin -u root -p'oldPassword' password 'newPassword'
    # The debian-sys-maint password is found here - /etc/mysql/debian.cnf
    $ sudo mysqladmin -u debian-sys-maint -p'oldPassword' password 'newPassword'
    # The zmuser password is found here - /etc/zm/zm.conf
    $ sudo mysqladmin -u zmuser -p'oldPassword' password 'newPassword'
    $ sudo sed -i -r "s#^(ZM_DB_PASS=).*#\1newPassword#" /etc/zm/zm.conf
    $ sudo sed -i -r "s#^(password =).*#\1 newPassword#" /etc/mysql/debian.cnf
    $ sudo systemctl restart mysql
    $ sudo systemctl restart zoneminder

    # Once new passwords are set, secure mysql installation
    $ sudo mysql_secure_installation

    # Optional: Update Gui Password from mysql ( Can update from gui, easier that way)
    $ mysql -u root -p 
    MySql> show databases;
    MySql> use zm;
    MySql> select * from Users;
    MySql> update Users set Password="password" where Username="admin";
    Mysql> FLUSH PRIVILEGES;
    Mysql> exit

 
References
----------

    https://zoneminder.readthedocs.io/en/stable/userguide/gettingstarted.html
    https://zoneminder.readthedocs.io/en/stable/installationguide/ubuntu.html
    https://www.howtogeek.com/devops/how-to-create-and-use-self-signed-ssl-on-apache/
    https://www.how2shout.com/linux/how-to-install-zoneminder-on-ubuntu-22-04-20-04-lts/
    https://httpd.apache.org/docs/2.4/rewrite/remapping.html
    https://zoneminder.readthedocs.io/en/stable/userguide/options/options_email.html
    