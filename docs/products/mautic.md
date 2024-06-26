Mautic is an open source marketing automation platform. [AWS Marketplace: Mautic ](https://aws.amazon.com/marketplace/pp/prodview-cykzx7o3md2mw?sr=0-4&ref_=beagle&applicationId=AWSMPContessa)


Note:
-----
Please be aware that it takes a few minutes for the system to be up and running. The best way to check is to 
view the status check from the ec2 / instances / dashboard. If it says intializing, it is not ready yet. 

SSH Into the server:
----------------------
* Linux + MAC - add .pem key to ~/.ssh/id_rsa > change permisisons > chmod 400 id_rsa
* ssh core@ip-of-server 
* If using putty or mobaxterm make sure to convert .pem using puttygen.

Passwords - DB AND/OR User:
--------------------------
* ssh into server
* cat ~/.docker/.env
* This will display the randomly generated passwords for DB AND/OR User. 

Mautic:
--------
* How to access Mautic > https://ip-of-server
* This requires entering the database password found in .env > ssh into server > cat .docker/.env > copy and paste password.
* Then following the instructions , create a new admin account, and select your mail settings. You can now login.

Portainer - Manage Docker:
--------------------------
* How to access Portainer to manage your containers > https://ip-of-server:9443
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then run. > docker restart portainer
* Once logged into portainer, click get started and select local. You can manage docker from here. 

Docker - Update Containers: 
---------------------------
* Caution: Make sure to back up any data and test the update in a staging environment before running these commands on a production server.
* ssh into the server 
* cd .docker
* docker-compose down
* docker-compose pull
* docker-compose up -d

Docker - Redeploy: 
------------------
* Optional: Troubleshooting - If you have issues and want to rebuild, delete via portainer.
* Enable startup and reboot: sudo systemctl enable startup && sudo reboot

Manage Flatcar Linux: 
---------------------
* Optional: Manaully update Flatcar. Updates will happen automatically. 
* If you want to manually check for updates run this command: update_engine_client -update

References:
-----------

    https://docs.docker.com/
    https://docs.portainer.io/
    https://docs.mautic.org/en
    https://www.flatcar.org/docs/latest


