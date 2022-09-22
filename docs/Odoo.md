Odoo
=====

Odoo is an open source Ecommerce and business management platform. 

Install
-------

     $ sudo apt install -y postgresq postgresql-client
     $ sudo -u postgres createuser -s $USER 
     $ createdb $USER
     $ wget -O - https://nightly.odoo.com/odoo.key | suo apt-key add - 
     $ sudo  echo "deb http://nightly.odoo.com/15.0/nightly/deb/ ./" >> 
     /etc/apt/sources.list.d/odoo.list 
     $ sudo apt-get update && apt-get install -y odoo
     # Setup postgres create another user, required.
     $ odoo-bin
     # http://localhost:8069


References
----------

https://www.odoo.com/
https://www.odoo.com/documentation/15.0/administration/install.html
https://www.odoo.com/documentation/15.0/administration/install/install.html#running-odoo