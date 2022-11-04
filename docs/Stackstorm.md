Stackstorm
=====

Stackstorm is an open source event driven automation platform that can automate your enterprise infrastructure. 

Install
-------

     # Ubuntu 20.04 
     $ sudo apt update && sudo apt upgrade
     $ sudo apt install net-tools
     $ bash <(curl -sSL https://stackstorm.com/packages/install.sh) --user=st2admin --password=Ch@ngeMe  

Change password
---------------

     $ sudo htpasswd /etc/st2/htpasswd st2admin
     # Manage server apply changes
     $ sudo st2ctl restart

Manage Your Databases
---------------------


  
References
----------

     https://docs.stackstorm.com/
     https://docs.stackstorm.com/install/index.html 
     https://docs.stackstorm.com/authentication.html 
     https://docs.stackstorm.com/install/u20.html

