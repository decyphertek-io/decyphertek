Odoo is an open source ERP & CRM server. Manage all aspects of your business with Odoo, including Website, Ecommerce, Inventory managment, POS, etc. 

SSH Into the server:
--------------------
* Utilize Google SSH Console or setup ssh keys or password.

Login to Odoo:
---------------
* https://ip-of-server
* Accept the auto-generated self signed cert, you can add your own certs in /etc/apache2/sites-available/apache.conf later.
* Odoo is secure and allows the user to set the master password , DB Name & User login at first access.
* You can choose to use the randomly generated password or use your own.
* To change the randomly generated password, simply refresh the page and will generate a new one.
* Please fill in all the fields that it is asking: ( Make sure to save your password info. )
```
Master Password: ( Make your own , or refresh to regenerate a new one. )
Database Name: odoo
Email: ( Your Email )
Password: ( Your Password )
Phone Number: ( Optional - Your Phone Number )
Language: ( Your Language )
Country: ( Your Country )
* Select Create Database

```
* Please be patient , it takes a few minutes to initialize your chosen settings.
* Once complete it will redirect you to a login page:
```
https://IP-OF-Server/web/login
Email: ( Your Email)
Password: ( Your Password)
```
* Once Logged in , you will be taken to the apps page, select which ones to activate.
* Please be patient, after clicking activate , take a few minutes to install . 

View Modsec logs:
-----------------
* Test Modsec:
```
# From the Odoo server:
sudo tail -f /var/log/modsec_audit.log
# Then run from you host system terminal:
curl -I "http://IP-OF-SERVER/index.html?test=<script>alert(1)</script>"
```
* Modescurity is currently in Detect Mode Only, If you want to actively block, then make these changes:
```
sudo vim /etc/apache2/mods-enabled/security2.conf
    SecRuleEngine On
    # SecRuleEngine DetectionOnly 

sudo systemctl daemon-reload
sudo systemctl restart apache2
```

Security Features:
------------------
* Auditd - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Crowdsec - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Apache - https://httpd.apache.org/docs/
* Modsecurity - https://github.com/owasp-modsecurity/ModSecurity/wiki/Reference-Manual-(v2.x)
* Automated Updates - Crontab runs at reboot and at 3am every morning.

References:
-----------
* https://www.odoo.com/documentation/17.0/