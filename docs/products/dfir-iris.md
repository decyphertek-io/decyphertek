DFIR IRIS is a digital forensics and incident response software tool designed to assist cybersecurity professionals in 
managing and analyzing digital evidence from information security incidents. It offers features for evidence collection, 
timeline analysis, and reporting, streamlining the process of investigating and responding to cybersecurity threats.

SSH Into the server:
--------------------
* Linux + MAC - add .pem key to ~/.ssh/id_rsa > change permisisons > chmod 400 id_rsa
* ssh core@ip-of-server 
* If using putty or mobaxterm make sure to convert .pem using puttygen.

Passwords - DB AND/OR User:
----------------------------
* ssh into server
* Display the randomly generated passwords for DB AND/OR User:
```
cat ~/.iris-web/.env
```

DFIR IRIS:
------------
* https://ip-of-server
* username: administrator Password: Instance ID 
* Find the instance Id from Ec2 dashboard or from terminal:
```
curl -s http://169.254.169.254/latest/meta-data/instance-id
```
* Wazuh-IRIS Integration - https://github.com/nateuribe/Wazuh-IRIS-integration

Portainer - Manage Docker:
---------------------------
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

Manage Flatcar Linux: 
---------------------
* Optional: Manaully update Flatcar. Updates will happen automatically. 
* If you want to manually check for updates run this command: update_engine_client -update


References:
-----------
* https://docs.docker.com/
* https://docs.portainer.io/
* https://www.flatcar.org/docs/latest
* https://dfir-iris.org/
* https://docs.dfir-iris.org/
