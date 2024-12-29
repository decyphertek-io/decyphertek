LAMP stack is setup on Ubuntu 24.04, that includes Apache with ModSecurity WAF, OWASP ruleset, MySQL 
for database management, and PHP with Composer for dependency management. Webmin is included for easy 
server administration. The system is secured with UFW as the host firewall, CrowdSec for intrusion prevention, 
Auditd for detailed logging, and automated updates to ensure the server remains secure and up-to-date.
[Azure Marketplace: Lamp Stack + ModSec + Webmin ]()


Webmin:
-------
* Set password and login to Webmin:
```
sudo adduser username
sudo passwd username
https://<Your-Server-IP>:10000
user: username
pass: YOURPASSWORDHERE
```
* You can now manage your webserver from Webmin.

Apache:
-------
* Verify Apache is running:
```
sudo systemctl status apache2
```
* If there is issues, may need to restart:
```
sudo systemctl restart apache2
```
* The apache configuration file:
```
sudo vim /etc/apache2/apache2.conf
```

Modsecurity:
--------------
* SSH Into your server.
* To test Modsec rules, you can run the following commands.
```
sudo tail -f /var/log/modsec_audit.log
# Run from your host system
curl -I "http://IP-OF-SERVER/index.html?test=<script>alert(1)</script>"
```
* You should see logs generated on the activity.
* If you want to set Modsec from detect only to actively block, do the following:
```
sudo vim /etc/apache2/mods-enabled/security2.conf
    SecRuleEngine On
    #SecRuleEngine DetectionOnly 

:wq!

sudo systemctl daemon-reload
sudo systemctl restart apache2

```
* You should have uncommented SecRuleEngine On and commented #SecRuleEngine DetectionOnly 

Mysql:
-------
* Secure your Mysql installation:
```
sudo mysql_secure_installation
```
* Go through the steps and decide what configuration you want. 
* Basic MySQL Commands:
```
# Log into MySQL as root:
mysql -u root -p
# Create a new database:
CREATE DATABASE my_database;
# Show all databases:
SHOW DATABASES;
# Create a new user and grant privileges:
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON my_database.* TO 'newuser'@'localhost';
FLUSH PRIVILEGES;
# Delete a database:
DROP DATABASE my_database;
# Exit MySQL:
EXIT;
```

PHP:
----
* Get PHP and Composer versions:
```
composer --version
```
* TO Create a composer.json file in your project directory:
```
composer init
```
* Basic PHP Composer commands:
```
# Install a package:
composer require vendor/package-name
# Update dependencies:
composer update
# Remove a package:
composer remove vendor/package-name
# Autoload classes in your project:
composer dump-autoload
```

Security Features:
------------------
* Modsecurity - https://owasp.org/www-project-modsecurity/
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and at 3am daily.

References:
-----------
* https://ubuntu.com/blog/canonical-releases-ubuntu-24-04-noble-numbat
* https://apache.org/
* https://owasp.org/www-project-modsecurity/
* https://www.php.net/
* https://getcomposer.org/
* https://www.mysql.com/
* https://webmin.com/