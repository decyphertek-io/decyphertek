Vaultwarden is a lightweight, self-hosted password manager that provides a more resource-efficient alternative 
to the official Bitwarden server. It offers full compatibility with Bitwarden client applications, enabling 
users to manage their passwords securely across different platforms. Vaultwarden ensures strong encryption 
and security for user data. It is community-driven, customizable, and ideal for those seeking full control 
over their password management system.

Note:
-------
* Please be aware that it takes a few minutes for the system to be up and running. 

SSH Into the server:
--------------------
* Utilize Google SSH Console or setup ssh keys or password.

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
sudo su adminotaur
cd ~
docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here. 

Security Features:
--------------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and at 3am daily.

References:
-------------
* https://docs.docker.com/
* https://github.com/dani-garcia/vaultwarden


