CheckMK
=====

Modern Open Source network Monitoring solution. 
 
Install - OMD version 2.1.0p15.cfe
--------

     # Ubuntu 22.04 
     $ sudo apt update && sudo apt upgrade -y
     $ wget https://download.checkmk.com/checkmk/2.1.0p15/check-mk-free-2.1.0p15_0.jammy_amd64.deb
     $ sudo dpkg -i check-mk-free-2.1.0p15_0.jammy_amd64.deb
     # If fails due to dependencies, run the following
     $ sudo apt install -f
     $ omd version
     $ sudo omd create monitoring
     # Follow output Information regarding access. 
     $ sudo omd start monitoring
     # Ignore it pointing to your hostname
     # http://ip-address-here/monitoring
     # user : cmkadmin
     # pass: autogenerated
     # Change Password
     $ sudo omd su monitoring
     $ htpasswd -B -C 12 etc/htpasswd cmkadmin
     $ exit
     $ sudo omd restart monitoring

Enable HTTPS
------------

     $ sudo a2enmod ssl
     $ sudo systemctl restart apache2
     $ sudo openssl req -x509 -nodes -days 1095 -newkey rsa:2048 -keyout /etc/ssl/private/private-ssl.key -out /etc/ssl/certs/private-ssl.crt -subj "/C=US/ST=Any/L=Anytown/O=decyphertek-io/OU=adminotaur/CN=decyphertek"
     $ sudo vim /etc/apache2/sites-available/default-ssl.conf
     <VirtualHost *:443>
     ServerName 127.0.0.1
     DocumentRoot /var/www/html
     
     SSLEngine on
     SSLCertificateFile /etc/ssl/certs/private-ssl.crt
     SSLCertificateKeyFile /etc/ssl/private/private-ssl.key
     </VirtualHost>
     
     $ sudo vim /etc/apache2/sites-enabled/000-default.conf
     RewriteEngine On
     RewriteCond %{SERVER_PORT} !^443$
     RewriteRule (.*) https://%{HTTP_HOST}$1 [L]
     $ sudo a2ensite default-ssl.conf
     $ sudo systemctl reload apache2
     $ sudo systemctl restart apache2

Managing Data
-------------

     Note:
     Since version 3.2.0, Redis enters a special mode called protected mode when it is executed with the default configuration (binding all the interfaces) and without any password in order to access it. 

     # Can create an encryption key iwith a passphrase and schedule regular backups
     Login > Settings > Maintenance > Backups 

Installing Agents
-----------------

     # Select your OS version and download from:
     > Login > Setup > agents > Windows, Linux, Solaris, AIX 
     $ sudo dpkg -i check-mk*.deb
     $ sudo cmk-agent-ctl --help
     $ sudo cmk-agent-ctl register --help
     # find your hostname
     $ hostnamectl
     # On server make a hostname
     > login > setup > hosts > add host > save & go to connection test
     # On client run the following command that references the hostname created and is the hostname of the client.
     # This appears to be a limitation here , can set the /etc/hosts to refernce the hostname and IP.
     $ sudo vim /etc/hosts
     ip-of-server hostname
     $ sudo cmk-agent-ctl register --hostname hostname --server ip-of-server:8000 --site monitoring -U cmkadmin -P password --trust-cert
     # Ports - CheckMK queries agents on TCP port 6556 and SNMP simultaneously.
     
References
----------

     https://checkmk.com/download?edition=cre&version=stable