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
     # If you are using ufw allow access to port 1880
     $ sudo ufw allow 1880
     # http://<your-instance-ip>:1880/

Secure Node Red - Enabling HTTPS Access and Setting Password
----------------------------------------
     $ mkdir ~/.node-red/keys
     $ openssl req -x509 -nodes -days 1095 -newkey rsa:2048 -keyout ~/.node-red/keys/private-ssl.key -out ~/.node-red/keys/private-ssl.crt -subj "/C=US/ST=Any/L=Anytown/O=decyphertek-io/OU=adminotaur/CN=decyphertek"
     $ npm install bcryptjs
     $ cd ~/.node-red/
     $ node -e "console.log(require('bcryptjs').hashSync(process.argv[1], 8));" your-password-here
     # add  password hash to settings.js
     $ vim ~/.node-red/settings.js

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
                    username: "admin",
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
    
Apply your changes
------------------

     $ sudo systemctl daemon-reload
     $ sudo systemctl restart pm2-adminotaur.service
    
References
----------

     https://nodered.org/docs/getting-started/aws#running-on-aws-ec2-with-ubuntu
     https://nodered.org/docs/user-guide/runtime/securing-node-red
     https://nodered.org/docs/user-guide/runtime/securing-node-red#enabling-https-access
     https://nodered.org/docs/user-guide/runtime/securing-node-red#editor--admin-api-security
     https://nodered.org/docs/user-guide/runtime/securing-node-red#http-node-security
     https://flows.nodered.org/node/node-red-contrib-bcrypt