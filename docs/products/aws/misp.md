MISP (Malware Information Sharing Platform & Threat Sharing) is an open source cyber threat intelligence platform designed to improve the sharing of structured threat information among organizations. [AWS Marketplace: MISP ](https://aws.amazon.com/marketplace/pp/prodview-b3xkycy2fp5kw)


Note:
-----
* Please be patient , it can take 5-10 minutes for the system to be accessible, 

SSH Into the server:
--------------------
* Linux + MAC - add .pem key to 
```
~/.ssh/id_rsa
# change permisisons
chmod 400 id_rsa
ssh core@ip-of-server
```
* If using putty or mobaxterm make sure to convert .pem using puttygen.

Passwords - DB AND/OR User:
-------------------------
* ssh into server:
```
cat ~/.docker/.env
```
* This will display the randomly generated passwords for DB AND/OR User. 

MISP - Access The Server:
-------------------------
* Login > https://ip-of-server
```
Username: admin@misp 
Password: cat ~/.docker/.env | grep ADMIN_PASSWORD
```
* Get data feeds > Dashboard > Sync Actions > Feeds > Load Default feed metadata > select pencil indicator, enable , submit > Fetch & store all Feed Data
* Change Password > Dashboard > Administration > List users > select user > Set Password > Save: Edit User - Confirm with old password
* Troubleshooting > IF IP changes or no Public IP > Edit .env:
```
vim ~/.docker/.env 
BASE_URL=your-server-IP 
cd .docker 
docker-compose down 
docker-compose up -d
```

Portainer - Manage Docker:
---------------------------
* How to access Portainer to manage your containers:
```
https://ip-of-server:9443
```
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then run.
```
docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here. 

Manage Flatcar Linux: 
--------------------
* Optional: Manaully update Flatcar. Updates will happen automatically. 
* If you want to manually check for updates run this command: 
```
sudo update_engine_client -update
```

References:
-----------
* https://docs.docker.com/
* https://docs.portainer.io/
* https://www.flatcar.org/docs/latest
* https://www.misp-project.org/