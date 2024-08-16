OneDev is a powerful and simple DevOps platform that integrates Git server, CI/CD, kanban, and packages.
It offers comprehensive features such as Git-based version control, advanced issue tracking, and continuous 
integration/continuous deployment (CI/CD) pipelines for automated testing and deployment. Additionally, 
OneDev supports efficient code review processes, project documentation, and wiki pages. Its extensibility 
through plugins and a RESTful API allows for high customization to fit various development needs. OneDev 
aims to provide a seamless and efficient workflow for development teams. [GCP Marketplace: OneDev ](https://console.cloud.google.com/marketplace/product/server-build-415714/onedev)


Note:
-------
* Please be aware that it takes a few minutes for the system to be up and running. 

SSH Into the server:
--------------------
* Utilize Google SSH Console or setup ssh keys or password.

OneDev:
------------
* How to access OneDev:
```
https://ip-of-server
```
* Enter following Info to setup a new account:
```
Login Name *
Password *
Full Name * 
Email Address * 
# Select Next
Server URL: http://localhost:6610
# Select Finish
```
* Enable MFA For All Users : 
```
Login > Administration > Secuirty Settings > Toggle "Enable Two Factor Authentication"
```
* Please refer to Ondev Docs to get your devops environment setup: https://docs.onedev.io/category/tutorials

Nginx:
------
* You can manage your nginx config and SSL Certs:
```
sudo su adminotaur
cd ~
cd .docker/.config/
```
* You can modify these nginx configs , then restart the container:
```
docker restart nginx-reverse-proxy
```

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
* https://docs.portainer.io/
* https://docs.onedev.io




