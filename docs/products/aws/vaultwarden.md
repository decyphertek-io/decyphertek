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

Portainer - Manage Docker:
--------------------------
* How to access Portainer to manage your containers > https://ip-of-server:9443
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then run. 
```
docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here. 

Manage Flatcar Linux: 
---------------------
* Optional: Manaully update Flatcar. Updates will happen automatically. 
* If you want to manually check for updates run this command
```
sudo update_engine_client -update
```

References:
-----------
* https://docs.docker.com/ 
* https://www.flatcar.org/docs/latest 
* https://github.com/dani-garcia/vaultwarden 
