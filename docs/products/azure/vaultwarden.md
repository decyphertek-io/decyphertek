Vaultwarden is a lightweight, self-hosted password manager that provides a more resource-efficient alternative to the official Bitwarden server. It offers full compatibility with Bitwarden client applications, enabling users to manage their passwords securely across different platforms. Vaultwarden ensures strong encryption 
and security for user data. It is community-driven, customizable, and ideal for those seeking full control over their password management system. [Azure Marketplace: Vaultwarden ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/decyphertek.vaultwarden?tab=Overview)

Note:
-------
* Please be aware that it takes a few minutes for the system to be up and running. 

SSH Into the server:
--------------------
* Utilize Azure SSH settings to set your ssh keys AND/OR Password to ssh in. 

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
sudo docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here. 

References:
-------------
* https://docs.docker.com/
* https://github.com/dani-garcia/vaultwarden


