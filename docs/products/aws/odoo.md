Odoo is an open source ERP & CRM server. Manage all aspects of your business with Odoo, including Wordpress, Ecommerce, Inventroy managment, POS, elearning platform, and many business applications to choose from.[AWS Marketplace: Odoo 17 CE ](https://aws.amazon.com/marketplace/pp/prodview-rq7r2an4ojrtw?sr=0-9&ref_=beagle&applicationId=AWSMPContessa)


Note:
-----
Please be aware that it can take 5-10 minutes for the system to be accessible. 

SSH Into the server:
--------------------
* Linux + MAC - add .pem key to 
```
~/.ssh/id_rsa
# change permisisons
chmod 400 id_rsa
ssh semaphore@ip-of-server
```
* If using putty or mobaxterm make sure to convert .pem using puttygen.

Login to Odoo:
---------------

* https://ip-of-server
* Accecpt self signed cert, you can add your own certs in nginx conf latter.
* If you get an Nginx error, it means Odoo is still intializing, please be patient.
* Odoo is secure and allows the user to set the master password , DB Name & User login at first access.
* You can choose to use the randomly generated password or use your own.
* To change the randomly generated password, simply refresh the page and will generate a new one.
* Please fill in all the fields that it is asking
* Please be patient , it takes a few minutes to initialize your chosen settings.

Fix Reporting issue: ( Will be updated on next release):
--------------------------------------------------------
```
# From the terminal

sudo nano /etc/odoo/odoo.conf

# I added this line to the odoo.conf

wkhtmltopdf_path = /usr/local/bin/wkhtmltopdf

# Save an exit

sudo chown odoo:odoo /usr/local/bin/wkhtmltopdf

# From the Odoo Dashboard >  Enable System parameter report.url
* Settings > General Settings > Scroll Down > Developer tools > Activate Develope Mode >
* Settings > Technical > Paramaters > System Paramaters > new > Key: report.url value: http://127.0.0.1:8069 > manually save

# From the terminal

sudo systemctl restart odoo 

```

View Modsec logs:
-----------------

* sudo tail -f /var/log/modsec_audit.log
* Test if modsec works
* https://IP-OR-Domain/index.html?exec=/bin/bash

Renew Self signed certs:
------------------------

* sudo systemctl enable generate-cert.service
* sudo reboot

Security Features:
------------------

* Auditd - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Crowdsec - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Unattended Upgrades - https://decyphertek.readthedocs.io/en/latest/technotes/Unattended-Upgrades/
* Quad9 DNS - https://decyphertek.readthedocs.io/en/latest/technotes/Quad9/
* Nginx/Modsec - https://decyphertek.readthedocs.io/en/latest/technotes/Nginx/ 

Additonal Resources:
-------------------

* Odoo 17 Docs - https://www.odoo.com/documentation/17.0/