Node-RED
=====

"Node-RED is a programming tool for wiring together hardware devices, 
APIs and online services in new and interesting ways."

Install
-------

     $ sudo apt update 
     $ sudo su -c "curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -"
     $ curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash - 
     $ sudo apt-get install -y nodejs build-essential 
     $ sudo npm install -g --unsafe-perm node-red
     $ sudo npm install -g --unsafe-perm pm2
     $ pm2 start `which node-red` -- -v 
     $ pm2 save 
     $ pm2 startup
     # replace adminotaur with your username if different, pm2 startup outputs the command to run.
     $ sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u adminotaur --hp /home/adminotaur
     $ sudo systemctl enable pm2-adminotaur.service
     $ sudo systemctl start pm2-adminotaur.service
     $ sudo systemctl status pm2-adminotaur.service
     $ sudo ufw allow 1880
     # http://<your-instance-ip>:1880/

     # Secure Node Red - Work In progress.......
     $ vim ~/.node-red/settings.js 
     

References
----------

     https://nodered.org/docs/getting-started/aws#running-on-aws-ec2-with-ubuntu
     https://nodered.org/docs/user-guide/runtime/securing-node-red
     https://nodered.org/docs/user-guide/runtime/securing-node-red#enabling-https-access
     https://nodered.org/docs/user-guide/runtime/securing-node-red#editor--admin-api-security
     https://nodered.org/docs/user-guide/runtime/securing-node-red#http-node-security