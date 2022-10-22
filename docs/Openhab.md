Openhab
=====

A smart home that you own and control. Works with most modern data tech, as it 
inherits the same compatible technology. 

Cloud Install
--------------
   
     # Doesnt work based off the instructions provided? Trying to Mod, work in progress....
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
     # Doesnt work? Maybe Need to setup Nginx?
     $ sudo cp /home/ubuntu/openhabcloud/etc/nginx_openhabcloud.conf /etc/nginx/sites-available/default
     $ sudo vim /etc/nginx/sites-enabled/default
     server {
     #listen *:443;
     listen *:80;
     #ssl on;
     # ssl_certificate /etc/nginx/ssl/YOUR-KEY.crt;
     # ssl_certificate_key /etc/nginx/ssl/YOUR-KEY.key;
     #ssl_certificate /etc/nginx/ssl/YOUR-CER.crt;
     #ssl_certificate_key /etc/nginx/ssl/YOUR-KEY.key;

     server_name YOUR-DNS-NAME;

     #if ( $scheme = "http" ) {
     #    rewrite ^/(.*)$    https://$host/$1 permanent;
     #}

     charset utf-8;

     access_log /var/log/nginx/openhabcloud.org-access.log;
     error_log /var/log/nginx/openhabcloud-error.log;
     client_max_body_size 300m;

     location /css {
          alias  /home/ubuntu/openhabcloud/public/css;
          }
     location /js {
          alias /home/ubuntu/openhabcloud/public/js;
               }
     location /img {
          alias /home/ubuntu/openhabcloud/public/img;
               }
     location /bootstrap {
          alias /home/ubuntu/openhabcloud/public/bootstrap;
               }
     location /font-icons {
          alias /home/ubuntu/openhabcloud/public/font-icons;
               }
     location /fonts {
          alias /home/ubuntu/openhabcloud/public/fonts;
               }
     location /js-plugin {
          alias /home/ubuntu/openhabcloud/public/js-plugin;
               }
     location /staff/js-plugin {
          alias /home/ubuntu/openhabcloud/public/js-plugin;
               }
     location /downloads {
          alias /home/ubuntu/openhabcloud/public/downloads;
               }
     location / {
          proxy_pass http://localhost:3000;
          proxy_redirect off;
          proxy_http_version 1.1;
          proxy_set_header Host $host;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection "upgrade";
          proxy_set_header X-Real-IP $remote_addr ;
               proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for ;
          proxy_set_header X-Forwarded-Proto https;
          }

          #error_page 404 /404.html;

          # redirect server error pages to the static page /50x.html
          #
          error_page 500 502 503 504 /50x.html;
          location = /50x.html {
     root html;
          }
     }
     
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
