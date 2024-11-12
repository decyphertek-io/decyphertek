Uptime Kuma is a self-hosted monitoring tool designed to track the availability and performance of websites and services. 
It provides real-time status updates, customizable alerts, and a user-friendly dashboard to help users ensure their sites 
and services remain operational. [Azure Marketplace: Uptime Kuma ]( )

Note:
------
* Please be aware that it takes a few minutes for Uptime Kuma to be up and running.

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

Uptime Kuma:
-------------
* How to access Uptime-Kuma > https://ip-of-server
* Follow instrucitons to create a new account. 
* You can now add a website to monitor.

Portainer - Manage Docker:
--------------------------
* How to access Portainer to manage your containers > https://ip-of-server:9443
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, from terminal:
```
sudo su adminotaur
docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here. 


References:
------------
* https://docs.docker.com/
* https://docs.portainer.io/
* https://github.com/louislam/uptime-kuma