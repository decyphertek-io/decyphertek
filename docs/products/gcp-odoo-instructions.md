Odoo is an open source ERP & CRM server. Manage all aspects of your business with Odoo, including Website, Ecommerce, Inventory managment, POS, etc. [GCP Marketplace: Odoo 18 CE ](https://console.cloud.google.com/marketplace/product/server-build-415714/odoo-18-ce)


SSH Into the server:
--------------------
* Utilize OS-Login OR add ssh keys via security & Access > SSH Keys > ssh-rsa KEY adminotaur
```
ssh adminotaur@ip-of-server
# OR: If using OS Login
sudo su adminotaur
cd ~
```

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

Settings:
---------
* Email Signature: Dashboard > Top Right Icon > Preferences > Can customize Email Signature > Save
* Time Zone: Dashboard > Top Right Icon > Preferences > 1st - Set time zone from Linux Terminal:
```
timedatectl list-timezones
# Ex:
timedatectl list-timezones | grep New_York
sudo timedatectl set-timezone America/New_York
# From Odoo UI
Dashboard > Top Right Icon > Preferences > Select Timezone > EX: (America/New_York) > Save 
```
* MFA: Dashboard > Top Right Icon > Preferences > Account Security > Toggle 2FA 

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
* OSSEC HIDS - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/
* UFW - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Rsyslog - https://www.rsyslog.com/doc/index.html
* Apache - https://httpd.apache.org/docs/
* Modsecurity - https://github.com/owasp-modsecurity/ModSecurity/wiki/Reference-Manual-(v2.x)
* Automated Updates - Crontab runs at reboot and at 3am every morning.
* Security Reports:
```
# Daily Security report
sudo cat /var/log/decyphertek/security_report*
```

References:
-----------
* https://www.odoo.com/documentation/18.0/