Uptime Kuma is a self-hosted monitoring tool designed to track the availability and performance of websites and services. 
It provides real-time status updates, customizable alerts, and a user-friendly dashboard to help users ensure their sites 
and services remain operational. [GCP Marketplace: Uptime Kuma ](https://console.cloud.google.com/marketplace/product/server-build-415714/uptime-kuma)

Note:
------
* Please be aware that it takes a few minutes for Uptime Kuma to be up and running.

SSH Into the server:
--------------------
* Utilize OS-Login OR add ssh keys via security & Access > SSH Keys > ssh-rsa KEY core
```
ssh core@ip-of-server
# OR: If using OS Login
sudo su core
cd ~
```

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
docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here. 

Security:
---------
* Flatcar Linux - Immutable OS : https://www.flatcar.org/docs/latest/
* Auditd Logging : https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Nginx: https://nginx.org/en/docs/
* Iptables Firewall : https://linux.die.net/man/8/iptables
* Portainer: https://docs.portainer.io/


References:
------------
* https://docs.docker.com/
* https://github.com/louislam/uptime-kuma