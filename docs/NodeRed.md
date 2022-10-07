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
     $ sudo npm install bcryptjs
     $ pm2 start node-red
     $ pm2 save 
     $ pm2 startup
     # Your startup path may differ than mine, please adjust accordingly based on startup output.
     $ sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u adminotaur --hp /home/adminotaur
     $ sudo systemctl enable pm2-adminotaur.service
     $ sudo ufw allow 1880
     $ mkdir /home/$USER/.node-red/keys
     $ openssl req -x509 -nodes -days 1095 -newkey rsa:2048 -keyout /home/$USER/.node-red/keys/private-ssl.key -out /home/$USER/.node-red/keys/private-ssl.crt -subj "/C=US/ST=Any/L=Anytown/O=decyphertek-io/OU=adminotaur/CN=decyphertek"
     $ curl 'https://raw.githubusercontent.com/decyphertek-io/configs/main/settings.js' >> /home/adminotaur/.node-red/settings.js
     $ sudo systemctl daemon-reload
     $ sudo reboot
     # http://<your-instance-ip>:1880/
     # Please change default username and password. 
     User : adminotaur
     Pass: decyphertek

Secure Node Red - Enabling HTTPS Access and Setting Password
----------------------------------------
     
     $ node -e "console.log(require('bcryptjs').hashSync(process.argv[1], 8));" your-password-here
     # add  password hash to settings.js
     $ vim /home/$USER/.node-red/settings.js

     /** Option 1: static object */
     https: {
     key: require("fs").readFileSync('/home/$USER/.node-red/keys/privkey.pem'),
     cert: require("fs").readFileSync('/home/$USER/.node-red/keys/cert.pem')
     },
     
     /** The following property can be used to cause insecure HTTP connections to
      * be redirected to HTTPS.
      */
     requireHttps: true,

     /* The `pass` field is a bcrypt hash of the password.
      * See http://nodered.org/docs/security.html#generating-the-password-hash
      */
     httpNodeAuth: {user:"adminotaur",pass:"password-hash"},
     httpStaticAuth: {user:"adminotaur",pass:"password-hash"},
     
     # Secure Node Red - Editor & Admin API security
     adminAuth: {
          type: "credentials",
          users: [
               {
                    username: "adminotaur",
                    password: "password-hash",
                    permissions: "*"
        },
        {
            username: "username",
            password: "password-hash",
            permissions: "read"
        }
      ]
    }
     
    
References
----------

     https://nodered.org/docs/getting-started/aws#running-on-aws-ec2-with-ubuntu
     https://nodered.org/docs/user-guide/runtime/securing-node-red
     https://nodered.org/docs/user-guide/runtime/securing-node-red#enabling-https-access
     https://nodered.org/docs/user-guide/runtime/securing-node-red#editor--admin-api-security
     https://nodered.org/docs/user-guide/runtime/securing-node-red#http-node-security
     https://flows.nodered.org/node/node-red-contrib-bcrypt