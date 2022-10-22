Openhab
=====

A smart home that you own and control. Works with most modern data tech, as it 
inherits the same compatible technology. 

Cloud Install
--------------

     $ sudo apt-get update && sudo apt-get upgrade -y
     $ sudo apt-get install build-essential redis-server mongodb nginx python3 git
     $ sudo su -c "curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -" 
     $ curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
     $ sudo apt-get install -y nodejs 
     $ sudo npm install -g npm@latest
     $ cd  /home/$USER/ 
     $ git clone https://github.com/openhab/openhab-cloud.git
     $ cd openhab-cloud
     $ npm install
     $ redis-cli ping
     $ config-production.json -> config.json
     $ sudo node app.js
     http://localhost:3000

Experimental: pm2 to run Openhab Cloud
-------------------

     $ npm install pm2@latest -g 
     $ pm2 start app.js
     $ pm2 save
     $ pm2 startup

Debian Install 
--------------

     $ curl -fsSL "https://openhab.jfrog.io/artifactory/api/gpg/key/public" | gpg --dearmor > openhab.gpg 
     $ sudo mkdir /usr/share/keyrings 
     $ sudo mv openhab.gpg /usr/share/keyrings $ sudo chmod u=rw,g=r,o=r /usr/share/keyrings/openhab.gpg
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
