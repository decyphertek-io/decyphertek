Gitea is an opensource software development platform. [AWSMP: Decyphertek ](https://aws.amazon.com/marketplace/pp/prodview-s7ltetwxbukly?sr=0-21&ref_=beagle&applicationId=AWSMPContessa)

Note:
------
Please be aware that it takes a few minutes for the system to be up and running. The best way to check is to 
view the status check from the ec2 / instances / dashboard. If it says intializing, it is not ready yet. 

SSH Into the server:
---------------------
* Linux + MAC - add .pem key to ~/.ssh/id_rsa > change permisisons > chmod 400 id_rsa
* ssh core@ip-of-server 
* If using putty or mobaxterm make sure to convert .pem using puttygen.

Gitea Instructions:
---------------------
* How to access Gitea > https://ip-of-server
* Scroll down to Administrator Account Settings and set the usename and password. 
* Optional: Set your email config under email settings.
* Gitea uses port 222 to push/pull via ssh. Generate new ssh keys via ssh keygen. Upload public key to Gitea gui.
* Optional: Setup ssh psuh/pull > click top right icon > Select settings > Select SSH/GPG keys > Add Key 

Portainer - Manage Docker:
---------------------------
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
----------------------
* Optional: Manaully update Flatcar. Updates will happen automatically. 
* If you want to manually check for updates run this command: update_engine_client -update


References:
-------------

    https://docs.gitea.com/
    https://docs.docker.com/
    https://docs.portainer.io/
    https://www.flatcar.org/docs/latest