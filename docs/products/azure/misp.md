MISP (Malware Information Sharing Platform & Threat Sharing) is an open-source platform designed to enhance cybersecurity by improving the sharing of structured threat information among organizations. MISP is typically used to bolster threat intelligence for SIEM systems or during the triage of security incidents.

SSH Into the server:
--------------------
* Utilize Azure SSH settings to set your ssh keys AND/OR Password to ssh in. 

Passwords - DB AND/OR User:
-------------------------
* ssh into server
```
sudo cat /root/.docker/.env
```
* This will display the randomly generated passwords for DB AND/OR User. 

MISP - Access The Server:
-------------------------
* Login > https://ip-of-server
* Username: admin@misp Password: ( ADMIN_PASSWORD found at /root/.docker/.env )
* Get data feeds > Dashboard > Sync Actions > Feeds > Load Default feed metadata > select pencil indicator, enable , submit > Fetch & store all Feed Data
* Change Password > Dashboard > Administration > List users > select user > Set Password > Save: Edit User - Confirm with old password
* Troubleshooting > IF IP changes or no Public IP > Edit .env :
```
sudo su
cd /root/.docker/
vim .env 
    BASE_URL=your=server-IP 
/opt/bin/docker-compose down 
/opt/bin/docker-compose up -d

```

Portainer - Manage Docker:
---------------------------
* How to access Portainer to manage your containers > https://ip-of-server:9443
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then run: 
```
sudo docker restart portainer
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