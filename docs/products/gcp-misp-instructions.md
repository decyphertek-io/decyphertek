MISP (Malware Information Sharing Platform & Threat Sharing) is an open source threat intelligence platform designed to improve the sharing of structured threat information among organizations. [GCP Marketplace: Misp ](https://console.cloud.google.com/marketplace/product/server-build-415714/misp)


SSH Into the server:
--------------------
* Utilize OS-Login OR add ssh keys via security & Access > SSH Keys > ssh-rsa KEY core
```
ssh core@ip-of-server
# OR: If using OS Login
sudo su core
cd ~
```

Passwords - DB AND/OR User:
-------------------------
* ssh into server:
```
cat /home/core/.docker/.env
```
* This will display the randomly generated passwords for DB AND/OR User. 

MISP - Access The Server:
-------------------------
* Login > https://ip-of-server
```
Username: admin@misp 
Password: cat /home/core/.docker/.env | grep ADMIN_PASSWORD
```
* Get data feeds > Dashboard > Sync Actions > Feeds > Load Default feed metadata > select pencil indicator, enable , submit > Fetch & store all Feed Data
* Change Password > Dashboard > Administration > List users > select user > Set Password > Save: Edit User - Confirm with old password
* Troubleshooting > IF IP changes or no Public IP > Edit .env:
```
sudo su core
vim /home/core/.docker/.env 
BASE_URL=your=server-IP
:wq!
cd /home/core/.docker 
/opt/bin/docker-compose down 
/opt/bin/docker-compose up -d
```

Portainer - Manage Docker:
---------------------------
* How to access Portainer to manage your containers > https://ip-of-server:9443
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then from terminal:
```
sudo su core
docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here. 
* If you want to manage docker from the terminal:
```
sudo su core
docker ps
``` 

Security:
---------
* Flatcar Linux - Immutable OS : https://www.flatcar.org/docs/latest/
* Auditd Logging : https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Iptables Firewall : https://linux.die.net/man/8/iptables
* Portainer: https://docs.portainer.io/


References:
-----------
* https://docs.docker.com/
* https://www.misp-project.org/