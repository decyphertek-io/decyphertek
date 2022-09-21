IDS Tower
=====

Open Source Surricata Gui.

Install
-------

     $ wget https://download.idstower.com/packages/idstower_latest.deb
     $ sudo apt install gdebi
     $ sudo gdebi idstower_latest.deb
     <OR>
     # GET FREE LICENSE KEY from website, sign up. 
     $ sudo wget -qO - https://download.idstower.com/repos/apt/idstower.key | sudo apt-key add -
     $ echo "deb [arch=amd64] https://download.idstower.com/repos/apt stable main" | sudo tee /etc/apt/sources.list.d/idstower.list
     $ sudo apt-get update
     $ sudo apt install mariadb-server ansible sshpass -y
     $ sudo systemctl enable mariadb.service
     $ sudo systemctl start mariadb.service
     $ sudo systemctl status mariadb.service
     $ sudo /usr/bin/mysql_secure_installation
     $ sudo mariadb
     $ GRANT ALL ON *.* TO '**USERNAME**'@'localhost' IDENTIFIED BY '**PASSWORD**' WITH GRANT OPTION;
     $ FLUSH PRIVILEGES;
     $ exit
     $ sudo apt install idstower -y
     $ sudo vim /opt/idstower/appsettings.json
     # set the LicenseKey key value
     # set the URL key value with the url or IP
     # set the MySQL Database settings 
     $ cd /opt/idstower/ 
     $ sudo ./IDSTower --init-database
     $ sudo ./IDSTower -a username
     $ sudo chown -R idstower:idstower /var/log/idstower/*
     $ sudo systemctl enable idstower.service
     $ sudo systemctl start idstower.service
     $ sudo systemctl status idstower.service
     

References
-----------

     https://idstower.com/docs/download.html
     https://www.idstower.com/docs/installation/install_ubuntu20.html