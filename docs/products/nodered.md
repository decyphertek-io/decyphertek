SSH into your server ( Please read AWS docs on ssh keys if you are lost )
$ ssh adminotaur@ip-of-server
Login to Node Red Dashboard
https://ip-of-server:1880
user: adminotaur
pass: decyphertek
Change Password and update users
$ node -e "console.log(require('bcryptjs').hashSync(process.argv[1], 8));" your-password-here
add  password hash to settings.js
$ vim /home/$USER/.node-red/settings.js
See Decyphertek Read the Docs for more verbose information

Node Red is an event driven automation platform written in Java Script. 

Nodered AWS Setup:
-----------------

    SSH into your server ( Please read AWS docs on ssh keys if you are lost )
    $ ssh adminotaur@ip-of-server
    Login to Node Red Dashboard
    https://ip-of-server:1880
    user: adminotaur
    pass: decyphertek
    Change Password and update users
    $ node -e "console.log(require('bcryptjs').hashSync(process.argv[1], 8));" your-password-here
    add  password hash to settings.js
    $ vim /home/$USER/.node-red/settings.js
  
  
References:
------------

    https://nodered.org/docs/
    https://decyphertek.readthedocs.io/en/latest/technotes/NodeRed/
