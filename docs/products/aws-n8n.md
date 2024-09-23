N8N is an open-source workflow automation tool that enables users to connect various apps and services without extensive coding. It features a visual interface for designing workflows, allowing users to automate tasks and data transfers easily. With a rich library of integrations, n8n empowers individuals and businesses to streamline their processes and enhance productivity. [AWS Marketplace: N8N ](https://aws.amazon.com/marketplace/pp/prodview-pg3ywjgtjc24w?sr=0-2&ref_=beagle&applicationId=AWSMPContessa)
    
Note:
----
* Please be aware that it takes a few minutes for the system to be up and running.
* The best way to check is to view the status check from the ec2 / instances / dashboard.
* If it says intializing, it is not ready yet.

SSH Into the server:
-------------------
* Linux + MAC - add .pem key to ~/.ssh/id_rsa > change permisisons > chmod 400 id_rsa
```    
ssh core@ip-of-server
```
* If using putty or mobaxterm make sure to convert .pem using puttygen.

N8N server setup:
-----------------
* https://ip-of-server
* Setup: Enter Email , First Name , Last name , and Password
* Customize: Choose your options.
* Create a workflow and Save.

Portainer - Manage Docker:
-------------------------
* How to access Portainer to manage your containers:
```
https://ip-of-server:9443
```
* Follow the instructions to create a new admin account.
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then run: 
```
docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here.

Optional:
-------- 
* Manaully update Flatcar. Updates will happen automatically.
* If you want to manually check for updates run this command: 
```
update_engine_client -update
```

References:
-----------
* https://docs.n8n.io/
* https://docs.docker.com/
* https://docs.portainer.io/
* https://www.flatcar.org/docs/latest