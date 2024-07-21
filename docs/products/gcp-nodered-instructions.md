Node Red is an event driven automation platform written in Java Script.[Google Cloud Marketplace: Nodered ]()

NodeRed - Login:
-----------------
* SSH into your server 
* Retrieve your password:
* sudo cat /home/adminotaur/password.txt
* Login to Node Red Dashboard:
```
https://ip-of-server:1880
username: adminotaur
password: ( See password.txt )
```

Optional: NodeRed - Change Password:
--------------------------
* SSH Into your server and login to as adminotaur user:
```
sudo su adminotaur
cd ~
```
* Run the following command to generate a password hash:
```
node -e "console.log(require('bcryptjs').hashSync(process.argv[1], 8));" your-password-here
```
* Add password the hash to settings.js under adminAuth , httpNodeAuth , & httpStaticAuth.
```
vim /home/adminotaur/.node-red/settings.js

adminAuth: {
    type: "credentials",
    users: [
        {
            username: "adminotaur",
            password: "PASSWORD-HASH-HERE",
            permissions: "*"
        }
    ]
},


httpNodeAuth: {user:"adminotaur",pass:"PASSWORD-HASH-HERE"},
httpStaticAuth: {user:"adminotaur",pass:"PASSWORD-HASH-HERE"},


```
* Apply the changes:
```
sudo systemctl daemon-reload
sudo systemctl restart pm2-adminotaur.service
```

NodeRed - Configuration:
------------------------
* When adding configuration nodes or any connections, you may need to open firewall ports via ufw and AWS security group.
* To see current firewall rules - ssh into your server and run the following:
```
sudo ufw status numbered
```
* EX: allow a firewall rule ( Port=1883 Protocol=tcp )
```
sudo ufw allow 1883/tcp 
```
* https://nodered.org/docs/user-guide/editor/workspace/nodes#configuration-nodes
* Troubleshooting: Check if ufw is blocking traffic : 
```
sudo less /var/log/ufw* | grep 'BLOCK'
```
* Troubleshooting: If all fails temporarily disable firewall:
```
#disable
sudo ufw disable 
#enable 
sudo ufw enable 
```

NodeRed - Security Features:
--------------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and at 3am daily.

References:
------------

* https://nodered.org/docs/
