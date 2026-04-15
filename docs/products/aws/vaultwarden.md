Vaultwarden is a self-hosted password manager that allows users to securely store and manage their passwords and sensitive information while retaining complete control over their data. It is an open-source alternative to Bitwarden, designed for easy deployment and management. With features such as end-to-end encryption, user management, and password sharing capabilities, Vaultwarden provides a robust solution for individuals and teams looking to enhance their data privacy without relying on third-party services. [AWS Marketplace: Vaultwarden ](https://aws.amazon.com/marketplace/pp/prodview-lw5oi2w6y3uyu?sr=0-1&ref_=beagle&applicationId=AWSMPContessa)

Note:
-----
Please be aware that it can take 5-10 minutes for the system to be accessible. 

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

Vaultwarden:
------------
* How to access Vaultwarden > https://ip-of-server 
* Select create a new account and follow the instructions:
* Optional: Enable MFA - Login > Account Settings > Security > Two Step Login > Select and enable your MFA.
* You can now import or add your passwords. 

Podman:
-------
* Podman is a daemonless, rootless container engine used to run Vaultwarden and Nginx securely.
* Check running containers:
```
podman ps
```
* Update containers - ssh into the server then run:
```
cd ~/.podman
podman-compose down
podman-compose pull
podman-compose up -d
```
* View container logs:
```
podman logs nginx-reverse-proxy
podman logs vaultwarden
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

Portainer - Manage Docker ( Used Before 04/14/26):
--------------------------
* This has been replaced in newer rleeases, due to the community version limiting functions. 
* How to access Portainer to manage your containers > https://ip-of-server:9443
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then run. 
```
docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here. 

Docker - Update Containers ( Used Before 4/14/26 ): 
---------------------------
* Caution: Make sure to back up any data and test the update in a staging environment before running these commands on a production server.
* ssh into the server 
```
cd .docker
/opt/bin/docker-compose down
/opt/bin/docker-compose pull
/opt/bin/docker-compose up -d
```

Manage Flatcar Linux ( Used Before 4/14/26 ): 
---------------------
* Optional: Manaully update Flatcar. Updates will happen automatically. 
* If you want to manually check for updates run this command
```
sudo update_engine_client -update
```

References:
-----------
* https://github.com/dani-garcia/vaultwarden
* https://docs.podman.io/en/latest/
* https://docs.fedoraproject.org/en-US/fedora-coreos/
* https://docs.docker.com/
* https://www.flatcar.org/docs/latest
