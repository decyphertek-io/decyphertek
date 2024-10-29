Node Red is an event driven automation platform written in Java Script.[AWS Marketplace: Nodered ](https://aws.amazon.com/marketplace/pp/prodview-pkaxmirrhshze?sr=0-3&ref_=beagle&applicationId=AWSMPContessa)

NodeRed - AWS Setup:
-----------------

* SSH into your server ( Please read AWS Basics mentioned below if you are stuck . )
* ssh adminotaur@ip-of-server
* Login to Node Red Dashboard
* https://ip-of-server:1880
* user: adminotaur
* V3.0 pass: decyphertek
* V3.1.3 Pass: instanceID
* Find the instance Id from Ec2 dashboard or from terminal - curl -s http://169.254.169.254/latest/meta-data/instance-id

NodeRed - Change Password
-------------------

* Run the following command to generate a password hash
* node -e "console.log(require('bcryptjs').hashSync(process.argv[1], 8));" your-password-here
* add password hash to settings.js under adminAuth:  ( Line 618 )
* vim /home/adminotaur/.node-red/settings.js
* Optional: Enable API - uncomment block //adminAuth: in settings.js ( Line 72 ) - https://nodered.org/docs/api/admin/oauth
* sudo systemctl daemon-reload
* sudo systemctl restart pm2-adminotaur.service

NodeRed - Configuration:
------------------------

* When adding configuration nodes or any connections, you may need to open firewall ports via ufw and AWS security group.
* To see current firewall rules - ssh into your server ssh adminotaur@ip-of-server and run the following
* sudo ufw status numbered
* EX: allow a firewall rule ( Port=1883 Protocol=tcp )
* sudo ufw allow 1883/tcp 
* https://nodered.org/docs/user-guide/editor/workspace/nodes#configuration-nodes
* Troubleshooting: Check if ufw is blocking traffic : sudo less /var/log/ufw* | grep 'BLOCK'
* Troubleshooting: If all fails temporarily disable firewall - sudo ufw disable ( re-enable : sudo ufw enable )

Nodered - Upgrade:
------------------

* Run the following commands to update Node-red
* sudo systemctl stop pm2-adminotaur
* sudo npm install -g --unsafe-perm node-red
* cd .nodered/
* npm update
* sudo systemctl start pm2-adminotaur

NodeRed - Security Features:
--------------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and at 1am daily.

AWS Basics:
-----------

* https://decyphertek.readthedocs.io/en/latest/products/aws-basics/

References:
------------

    https://nodered.org/docs/
    https://decyphertek.readthedocs.io/en/latest/technotes/NodeRed/
