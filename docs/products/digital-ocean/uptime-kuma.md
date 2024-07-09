Uptime Kuma is an opensource Web monitoring tool. [Digital ocean Marketplace: Uptime Kuma ](https://marketplace.digitalocean.com/apps/uptime-kuma)

Note:
-----
Please be aware that it takes a few minutes for the system to be up and running. 

SSH Into the server:
----------------------
* Linux + MAC - add .pem key to ~/.ssh/id_rsa > change permisisons > chmod 400 id_rsa
* ssh root@ip-of-server 
* If using putty or mobaxterm make sure to convert .pem using puttygen.

Passwords - DB AND/OR User:
--------------------------
* ssh into server
* cat ~/.docker/.env
* This will display the randomly generated passwords for DB AND/OR User. 

Uptime Kuma:
-------------
* How to ssh into your server > ssh root@ip-of-server
* How to access Portainer to manage your containers > https://ip-of-server:9443
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough
* if this happenes you need to restart the container, ssh into the server, then run. > docker restart portainer
* Once logged into portainer, click get started and select local. You can manage docker from here. 
* How to access Uptime-Kuma > https://ip-of-server
* Follow instrucitons to create a new account. 
* Optional: Troubleshooting - If for some reason the startup script didnt run on first boot, please enable startup and reboot.
* Optional: Troubleshooting - sudo systemctl enable startup && sudo reboot

Portainer - Manage Docker:
--------------------------
* How to access Portainer to manage your containers > https://ip-of-server:9443
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then run. > docker restart portainer
* Once logged into portainer, click get started and select local. You can manage docker from here. 

References:
-----------

* https://docs.docker.com/
* https://docs.portainer.io/
* https://www.flatcar.org/docs/latest
* https://github.com/louislam/uptime-kuma