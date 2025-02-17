DFIR IRIS is an incident response platform designed to assist cybersecurity professionals in managing and analyzing alerts from information security incidents. It offers Incident reponse, timeline analysis, and reporting, streamlining the process of investigating and responding to cybersecurity threats. [AWS Marketplace: DFIR IRIS ](https://aws.amazon.com/marketplace/pp/prodview-jbgytgbtdymze?sr=0-17&ref_=beagle&applicationId=AWSMPContessa)

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

Passwords - DB AND/OR User:
---------------------------
* ssh into server
```
cat .docker/.env
```
* This will display the randomly generated passwords for DB AND/OR User.
* To find just the DFIR IRIS login username and password:
```
cat .docker/.env | grep -E 'IRIS_ADM_PASSWORD|IRIS_ADM_USERNAME'
```

DFIR IRIS:
----------
```
https://ip-of-server 
username: administrator Password: ( see .env mentioned above )
Wazuh-IRIS Integration - https://github.com/nateuribe/Wazuh-IRIS-integration 
```

Portainer - Manage Docker:
--------------------------
* How to access Portainer to manage your containers:
```
https://ip-of-server:9443 
```
* Follow the instructions to create a new admin account.
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then run : 
```
docker restart portainer
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
* https://dfir-iris.org/ 
* https://docs.dfir-iris.org/ 
