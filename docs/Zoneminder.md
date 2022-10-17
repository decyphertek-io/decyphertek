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
    $ sudo chown root:www-data /etc/zm/zm.conf 
    $ sudo chown -R www-data:www-data /usr/share/zoneminder/

Configure Apache 
----------------

    $ sudo a2enmod cgi
    $ sudo a2enmod rewrite
    $ sudo a2enconf zoneminder
    $ sudo a2enmod expires
    $ sudo a2enmod headers

Manage Zoneminder
-------------------------

    $ sudo systemctl enable zoneminder
    $ sudo systemctl start zoneminder

Edit Timezone
--------------

    $ sudo vim /etc/php/7.2/apache2/php.ini
    [Date]
    ; Defines the default timezone used by the date functions
    ; http://php.net/date.timezone
    date.timezone = America/New_York

Reload Apache
-------------

    $ systemctl reload apache2

Login
-----

    http://hostname_or_ip/zm

Api 
---

    http://hostname_or_ip/zm/api/host/getVersion.json

References
----------

    https://zoneminder.readthedocs.io/en/stable/installationguide/ubuntu.html