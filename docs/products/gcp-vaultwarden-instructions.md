Vaultwarden is a lightweight, self-hosted password manager that provides a more resource-efficient alternative 
to the official Bitwarden server. It offers full compatibility with Bitwarden client applications, enabling 
users to manage their passwords securely across different platforms. Vaultwarden ensures strong encryption 
and security for user data. It is community-driven, customizable, and ideal for those seeking full control 
over their password management system. [GCP Marketplace: Vaultwarden ](https://console.cloud.google.com/marketplace/product/server-build-415714/vaultwarden)


Note:
-------
* Please be aware that it takes a few minutes for the system to be up and running. 

SSH Into the server:
--------------------
* Utilize OS-Login OR add ssh keys via security & Access > SSH Keys > ssh-rsa KEY core
```
ssh core@ip-of-server
# OR: If using OS Login
sudo su core
cd ~
```

Vaultwarden:
------------
* How to access Vaultwarden 
```
https://ip-of-server
```
* Select create a new account and follow the Instructions.
* Optional: Enable MFA - Login > Account Settings > Security > Two Step Login > Select and enable your MFA.  

Portainer:
----------
* How to access Portainer to manage your containers:
``` 
https://ip-of-server:9443
```
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough, if this happens ssh into your server & run:
```
sudo su core
cd ~
docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here. 

Security:
---------
* Flatcar Linux - Immutable OS : https://www.flatcar.org/docs/latest/
* Auditd Logging : https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Nginx: https://nginx.org/en/docs/
* Iptables Firewall : https://linux.die.net/man/8/iptables
* Portainer: https://docs.portainer.io/

References:
-------------
* https://docs.docker.com/
* https://github.com/dani-garcia/vaultwarden


