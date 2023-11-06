Please be aware that it takes a few minutes for the system to be up and running. The best way to check is to 
view the status check from the ec2 / instances / dashboard. If it says intializing, it is not ready yet. 

SSH Into the server:
1. Linux + MAC - add .pem key to ~/.ssh/id_rsa > change permisisons > chmod 400 id_rsa
2. ssh core@ip-of-server 
3. If using putty or mobaxterm make sure to convert .pem using puttygen.

Passwords - DB AND/OR User:
1. ssh into server
2. cat ~/.docker/.env
3. This will display the randomly generated passwords for DB AND/OR User. 

* Server Purchased  *
1. We are working on providing specific server instructions in Read The Docs
2. Please reference your instructions on AWS Marketplace for your purchased server.
3. Your welcome to provide any feedback , see contact.

Portainer - Manage Docker:
1. How to access Portainer to manage your containers > https://ip-of-server:9443
2. Follow the instructions to create a new admin account. 
3. Caution - Portainer can timeout if you dont create an account fast enough
4. If this happens you need to restart the container, ssh into the server, then run. > docker restart portainer
5. Once logged into portainer, click get started and select local. You can manage docker from here. 

Docker - Update Containers: 
* Caution: Make sure to back up any data and test the update in a staging environment before running these commands on a production server.
1. ssh into the server 
2. cd .docker
3  docker-compose down
4. docker-compose pull
5. docker-compose up -d

Docker - Redeploy: 
1. Optional: Troubleshooting - If you have issues and want to rebuild, delete via portainer.
2. Enable startup and reboot: sudo systemctl enable startup && sudo reboot

Manage Flatcar Linux: 
1. Optional: Manaully update Flatcar. Updates will happen automatically. 
2. If you want to manually check for updates run this command: update_engine_client -update


*References*
https://docs.docker.com/
https://docs.portainer.io/
https://www.flatcar.org/docs/latest
