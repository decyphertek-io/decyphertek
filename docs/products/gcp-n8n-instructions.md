N8N is an open-source workflow automation tool that allows users to connect various apps, services, and APIs to automate tasks and processes without writing code. It provides a visual interface to create complex workflows by linking different actions, such as sending emails, processing data, or interacting with third-party services. N8N is highly customizable and can be self-hosted, making it a flexible solution for businesses and developers looking to automate their workflows. [GCP Marketplace: N8N ](https://console.cloud.google.com/marketplace/product/server-build-415714/n8n)

SSH Into the server:
--------------------
* Utilize Google SSH Console or setup ssh keys or password.

N8N:
-------------------
* Go to your web browser and enter:
```
https://ip-of-server
```
* Setup: Enter Email , First Name , Last name , and Password
* Customize: Choose your options.
* Create a workflow and Save.

Portainer:
----------
* How to access Portainer to manage your containers:
``` 
https://ip-of-server:9443
```
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then run:  
```
sudo su adminotaur
docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here. 

Security Features:
------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and at 3am daily.

References:
-------------
* https://docs.n8n.io/
* https://docs.docker.com/
* https://docs.portainer.io/
