MISP (Malware Information Sharing Platform & Threat Sharing) is an open source cyber threat intelligence platform designed to improve the sharing of structured threat information among organizations. [AWS Marketplace: MISP ](https://aws.amazon.com/marketplace/pp/prodview-b3xkycy2fp5kw)


Note:
-----
* Please be patient , it can take 5-10 minutes for the system to be accessible.
* Podman used after 4/16/26 , if using older version use .docker & docker-compose instead

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
cat ~/.podman/.env
```
* This will display the randomly generated passwords for DB AND/OR User. 

MISP - Access The Server: 
-------------------------
* Login > https://ip-of-server
```
Username: admin@misp 
Password: cat ~/.podman/.env | grep ADMIN_PASSWORD
```
* Get data feeds > Dashboard > Sync Actions > Feeds > Load Default feed metadata > select pencil indicator, enable , submit > Fetch & store all Feed Data
* Change Password > Dashboard > Administration > List users > select user > Set Password > Save: Edit User - Confirm with old password
* Troubleshooting > IF IP changes or no Public IP > Edit .env:
```
vi ~/podman./.env 
BASE_URL=your-server-IP 
cd .podman 
podman-compose down 
podman-compose up -d
```

Podman:
-------
* Podman is a daemonless, rootless container engine used to run MISP, MariaDB, Valkey (Redis-compatible), and supporting services securely.
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
podman logs redis
podman logs mariadb
podman logs misp-core
podman logs misp-modules
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

Manage Flatcar Linux: ( Before 4/16/26 )
--------------------
* Optional: Manaully update Flatcar. Updates will happen automatically. 
* If you want to manually check for updates run this command: 
```
sudo update_engine_client -update
```

References:
-----------
* https://www.misp-project.org/
* https://docs.podman.io/en/latest/
* https://docs.fedoraproject.org/en-US/fedora-coreos/
* https://docs.docker.com/
* https://docs.portainer.io/
* https://www.flatcar.org/docs/latest