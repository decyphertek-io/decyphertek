Odoo
=====

Odoo is an open source Ecommerce and business management platform. 

Install
-------

     $ sudo apt update
     $ sudo apt install -y python3-pip  
     $ sudo -H python3 -m pip install  xlwt num2words wkhtmltopdf
     $ sudo apt install postgresql -y
     $ wget -q -O - https://nightly.odoo.com/odoo.key | sudo gpg --dearmor -o /usr/share/keyrings/odoo-archive-keyring.gpg
     $ echo 'deb [signed-by=/usr/share/keyrings/odoo-archive-keyring.gpg] https://nightly.odoo.com/16.0/nightly/deb/ ./' | sudo tee /etc/apt/sources.list.d/odoo.list
     $ sudo apt-get update && sudo apt-get -y install odoo
     $ sudo systemctl status odoo
     $ sudo vim /etc/odoo/odoo.conf
     # change admin password to be able to create a database on first login	
     # http://localhost:8069
     # Optional: Setup Nginx reverse proxy. See docs . 


References
----------

     https://www.odoo.com/
     https://www.odoo.com/documentation/16.0/administration/install.html
     https://www.odoo.com/documentation/16.0/administration/install/install.html#running-odoo
     https://bobcares.com/blog/database-creation-error-access-denied-odoo/