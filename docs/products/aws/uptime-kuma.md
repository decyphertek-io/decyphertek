Uptime Kuma is a powerful open source web monitoring tool designed to track the availability and performance of your websites, services, and APIs. With a clean and intuitive interface, it offers real-time status updates, customizable alerts, and detailed performance metrics. Uptime Kuma supports multiple monitoring protocols, including HTTP, HTTPS, TCP, and DNS, making it a versatile solution for ensuring your online services remain operational. Its self-hosted nature gives you full control over your monitoring environment, while features like multi-user support, status pages, and integrations with popular notification services (e.g., Slack, Telegram, Discord) make it an ideal choice for teams and individuals alike. [AWS Marketplace: Uptime Kuma ](https://aws.amazon.com/marketplace/pp/prodview-6ny3xloslkmh2?sr=0-1&ref_=beagle&applicationId=AWSMPContessa)


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

Uptime Kuma:
-------------
* How to access Uptime-Kuma > https://ip-of-server
* Setup Database > Select Embedded Mariadb
* Create the admin account , customize you username and password. 
* Create a monitor > Select Add Monitor ( Top Right ) > Fill in data. Thats it. 

(Optional) API:
--------------
* Login > Click user Icon > Settings > Api Keys > Add APi Key > Copy Api key
```
# EX: using Curl
curl -sk "https://IP-OR-DOMAIN/metrics" \
  --user ":APIKEY" | \
  grep -E 'monitor_(status|response_time)'
```

Podman:
-------
* Podman is a daemonless, rootless container engine used to run Uptime Kuma and Nginx securely.
* Check running containers:
```
podman ps
```
* Update containers — ssh into the server then run:
```
cd ~/.podman
podman-compose down
podman-compose pull
podman-compose up -d
```
* View container logs:
```
podman logs nginx-reverse-proxy
podman logs uptime-kuma
```

FCOS Linux:
-----------
* Fedora CoreOS (FCOS) is an automatically updating, minimal, container-focused operating system.
* Check SELinux status:
```
getenforce
```
* Check firewall rules:
```
sudo firewall-cmd --list-all
```
* Check audit logs:
```
sudo aureport --summary
```
* Install additional packages (requires reboot to apply):
```
sudo rpm-ostree install <package>
sudo systemctl reboot
```
* Check system status:
```
sudo systemctl status
```

Portainer - Manage Docker ( Used Before 3/31/26):
--------------------------
* This has been replaced by arcane in newer rleeases, due to the community version limiting functions. 
* How to access Portainer to manage your containers > https://ip-of-server:9443
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then run. 
```
docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here. 

Docker - Update Containers: ( Used Before 4/16/26):
---------------------------
* Caution: Make sure to back up any data and test the update in a staging environment before running these commands on a production server.
* ssh into the server 
```
cd .docker
/opt/bin/docker-compose down
/opt/bin/docker-compose pull
/opt/bin/docker-compose up -d
```

Manage Flatcar Linux: ( Used Before 4/16/26):
---------------------
* Optional: Manaully update Flatcar. Updates will happen automatically. 
* If you want to manually check for updates run this command
```
sudo update_engine_client -update
```

References:
-----------
* https://github.com/louislam/uptime-kuma
* https://docs.podman.io/en/latest/
* https://docs.fedoraproject.org/en-US/fedora-coreos/
* https://docs.docker.com/
* https://docs.portainer.io/
* https://www.flatcar.org/docs/latest
