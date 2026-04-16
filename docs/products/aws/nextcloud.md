Nextcloud is a self-hosted cloud suite and collaboration platform that provides secure business storage, document sharing, and real-time editing with full control over your data to ensure privacy. [AWS Marketplace: Nextcloud ](https://aws.amazon.com/marketplace/pp/prodview-7bloglkayfve2?sr=0-10&ref_=beagle&applicationId=AWSMPContessa)

SSH Into the server:
--------------------
1. Linux + MAC - add .pem key to ~/.ssh/id_rsa > change permisisons > chmod 400 id_rsa
2. ssh core@ip-of-server 
3. If using putty or mobaxterm make sure to convert .pem using puttygen.

Passwords - DB AND/OR User:
----------------------------
1. ssh into server
2. cat ~/.podman/.env
3. This will display the randomly generated passwords for DB AND/OR User. 

NextCloud - Setup:
------------------
* Login > https://ip-of-server
* Create an admin username and password ( There is no default set )
* Skip install Recommended Apps, this takes a long time to work. 
* If you want to download the recommended packages you can do it manually. 
* Optional: Login > Select Account Icon: Top Right > Select: Apps > Office & Text > Download & Enable: Calender , Contacts , Nextcloud Office , 
* Optional: Login > Select Account Icon: Top Right > Select: Apps > Social & COmmunication > Download & Enable: talk 

Podman:
-------
* Podman is a daemonless, rootless container engine used to run Nextcloud, MariaDB, and Nginx securely.
* Check running containers:
```
podman ps
```
* Update containers — ssh into the server then run:
```
cd ~/.podman
podman-compose down
podman-compose pull
podman-compose up -d
```
* View container logs:
```
podman logs nginx-reverse-proxy
podman logs mariadb
podman logs nextcloud
```

FCOS Linux:
-----------
* Fedora CoreOS (FCOS) is an automatically updating, minimal, container-focused operating system.
* Check SELinux status:
```
getenforce
```
* Check firewall rules:
```
sudo firewall-cmd --list-all
```
* Check audit logs:
```
sudo aureport --summary
```
* Install additional packages (requires reboot to apply):
```
sudo rpm-ostree install <package>
sudo systemctl reboot
```
* Check system status:
```
sudo systemctl status
```

Portainer - Manage Docker: ( Before 4/16/26 )
--------------------------
* How to access Portainer to manage your containers > https://ip-of-server:9443
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then run. > docker restart portainer
* Once logged into portainer, click get started and select local. You can manage docker from here. 

Manage Flatcar Linux: ( Before 4/16/26 )
---------------------
* Optional: Manaully update Flatcar. Updates will happen automatically. 
* If you want to manually check for updates run this command: update_engine_client -update


References:
-----------
* https://docs.nextcloud.com/
* https://docs.podman.io/en/latest/
* https://docs.fedoraproject.org/en-US/fedora-coreos/
* https://docs.docker.com/
* https://docs.portainer.io/
* https://www.flatcar.org/docs/latest
