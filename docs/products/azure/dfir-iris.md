DFIR IRIS is an incident response platform designed to assist cybersecurity professionals in managing and analyzing alerts from information security incidents. It offers Incident reponse, timeline analysis, and reporting, streamlining the process of investigating and responding to cybersecurity threats. [Azure Marketplace: DFIR IRIS ]()

Note:
-----
* It takes 5-10 minutes for DFIR IRIS to be accesible, please be patient.

SSH Into the server:
--------------------
* Utilize Azure SSH settings to set your ssh keys AND/OR Password to ssh in. 

Passwords - DB AND/OR User:
---------------------------
* ssh into server
```
sudo cat /root/.docker/.env
```
* This will display the randomly generated passwords for DB AND/OR User.
* To find just the DFIR IRIS login username and password:
```
sudo cat /root/.docker/.env | grep -E 'IRIS_ADM_PASSWORD|IRIS_ADM_USERNAME'
```

DFIR IRIS:
----------
```
https://ip-of-server 
username: administrator Password: ( see .env mentioned above )
Wazuh-IRIS Integration - https://github.com/nateuribe/Wazuh-IRIS-integration 
MISP Integration - https://docs.dfir-iris.org/latest/operations/modules/natives/IrisMISP/
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
* https://dfir-iris.org/ 
* https://docs.dfir-iris.org/ 