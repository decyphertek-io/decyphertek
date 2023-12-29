Node Red is an event driven automation platform written in Java Script. 

Nodered AWS Setup:
-----------------

    * SSH into your server ( Please read AWS docs on ssh keys if you are lost )
    * ssh adminotaur@ip-of-server
    * Login to Node Red Dashboard
    * https://ip-of-server:1880
    * user: adminotaur
    * pass: decyphertek
    * Change Password and update users
    * node -e "console.log(require('bcryptjs').hashSync(process.argv[1], 8));" your-password-here
    * add password hash to settings.js under adminAuth:  ( Line 618 )
    * vim /home/$USER/.node-red/settings.js
    * Optional: Enable API - uncomment block //adminAuth: in settings.js ( Line 72 )
    * sudo systemctl daemon-reload
    * sudo systemctl restart pm2-adminotaur.service

Node Red Configuration:
------------------------

    Be aware that ufw host firewall is enable. When adding configuration nodes or any connections, you may need 
    to open firewall ports via ufw and AWS security group.
    # To see current firewall rules - ssh into your server ssh adminotaur@ip-of-server and run the following
    $ sudo ufw status numbered
    # EX: allow a firewall rule ( Port=1883 Protocol=tcp )
    $ sudo ufw allow 1883/tcp 
    # https://nodered.org/docs/user-guide/editor/workspace/nodes#configuration-nodes

NodeRed Security Features:
--------------------------

    https://decyphertek.readthedocs.io/en/latest/products/debian-security/

AWS Basics:
-----------

    https://decyphertek.readthedocs.io/en/latest/products/aws-basics/

References:
------------

    https://nodered.org/docs/
    https://decyphertek.readthedocs.io/en/latest/technotes/NodeRed/
