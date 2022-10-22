Openhab
=====

A smart home that you own and control. Works with most modern data tech, as it 
inherits the same compatible technology. OPENHAB NEEDS REHAB , Their instructions
do not work? ( Tested on Ubuntu 22.04(MongoDB Fails) && Debain 11 ( installs, doesnt work?))

Cloud Install
--------------
   
     # Doesnt work based off the instructions provided? 
     $ sudo apt-get update && sudo apt-get upgrade -y
     $ curl -fsSL https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
     $ echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
     $ sudo su -c "curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -" 
     $ curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
     $ sudo apt update
     $ sudo apt-get install -y build-essential redis-server mongodb-org nodejs nginx python3 git
     $ sudo npm install -g npm@latest
     $ sudo systemctl enable mongod
     $ sudo systemctl start mongod
     $ sudo systemctl enable redis
     $ sudo systemctl start redis
     $ cd  /home/$USER/ 
     $ git clone https://github.com/openhab/openhab-cloud.git
     $ cd openhab-cloud
     $ sudo npm install --force
     $ sudo npm audit fix --force
     $ redis-cli ping
     $ cp config-production.json config.json
     $ sudo npm install pm2@latest -g 
     $ pm2 start app.js
     $ pm2 save
     $ pm2 startup
     $ sudo cp /home/$USER/openhab-cloud/etc/nginx_openhabcloud.conf /etc/nginx/sites-available/default
     $ sudo cat /etc/nginx/sites-enabled/default
     $ sudo mkdir /etc/nginx/ssl
     $ sudo openssl req -x509 -nodes -days 1095 -newkey rsa:2048 -keyout /etc/nginx/ssl/openhabcloud.key -out /etc/nginx/ssl/openhabcloud.crt -subj "/C=US/ST=Any/L=Anytown/O=decyphertek-io/OU=adminotaur/CN=decyphertek"
     $ sudo systemctl restart nginx
     
     
     $ sudo systemctl restart pm2-adminotaur

     # Maybe try npm http server
     $ sudo npm install -g http-server
     $ cd ~/openhab-cloud/etc/
     $ http-server -p 3000
     # find out where the directories are and move nginx ones there . 
     
Debian Install 
--------------

     $ curl -fsSL "https://openhab.jfrog.io/artifactory/api/gpg/key/public" | gpg --dearmor > openhab.gpg 
     $ sudo mv openhab.gpg /usr/share/keyrings 
     $ sudo chmod u=rw,g=r,o=r /usr/share/keyrings/openhab.gpg
     $ echo 'deb [signed-by=/usr/share/keyrings/openhab.gpg] https://openhab.jfrog.io/artifactory/openhab-linuxpkg stable main' | sudo tee /etc/apt/sources.list.d/openhab.list
     $ sudo apt-get update
     $ sudo apt-get install openhab openhab-addons
     # http://openhab-device:8080

TroubleShooting
----------------

     $ sudo systemctl start openhab.service
     $ sudo systemctl status openhab.service
     $ sudo systemctl daemon-reload
     $ sudo systemctl enable openhab.service

Upgrade
--------

     $ sudo apt-get update 
     $ sudo apt-cache showpkg openhab
     $ sudo apt-get install openhab=[version]

OpenHabian Install
-------------------

     # Raspberry Pi & Balena Etcher
     $ wget https://github.com/openhab/openhabian/releases/download/v1.7.4b/openhabian-pi-raspios32-202208151955-gitbe9d23e-crc075defd9.img.xz
     # burn image to sd card using Balena Etcher
     # load and boot in Raspberry Pi
     # http://openhabian:8080/

References
----------

     https://www.openhab.org/
     https://www.openhab.org/docs/installation/linux.html
     https://github.com/openhab/openhab-cloud/blob/master/README.md
     https://www.openhab.org/docs/tutorial/first_steps.html
     https://github.com/openhab/openhabian/releases
