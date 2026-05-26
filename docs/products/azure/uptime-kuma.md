Uptime Kuma is a self-hosted monitoring tool designed to track the availability and performance of websites and services. It provides real-time status updates, customizable alerts, and a user-friendly dashboard to help users ensure their sites and services remain operational. [Azure Marketplace: Uptime Kuma ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/decyphertek.uptime-kuma?tab=Overview)


Note:
------
* After 5/25/26 uses podman instead of docker and requires the core user .
* After 5/25/26 Portainer is no longer used.
* After 5/25/26 Fedora CoreOS is used instead of FlatCar Linux
* After 5/25/26 Caddy and Coraza Waf is used instead of nginx. 
* Please be aware that it takes a few minutes for Uptime Kuma to be up and running.

SSH Into the server:
--------------------
* Please launch the VM with the core user.
* Utilize Azure SSH settings to set your ssh keys AND/OR Password to ssh in. 

Uptime Kuma: 
-------------
* How to access Uptime-Kuma > https://ip-of-server
* Setup Database > Select Embedded Mariadb
* Create the admin account , customize you username and password. 
* Create a monitor > Select Add Monitor ( Top Right ) > Fill in data. Thats it. 

Podman: 
-------
* Podman is a daemonless, rootless container engine used to run Uptime Kuma and Nginx securely.
* Check running containers:
```
podman ps
```
* Update containers — ssh into the server then run:
```
cd ~/opt/.podman/
podman-compose down
podman-compose pull
podman-compose up -d
```
* View container logs:
```
podman logs caddy-ingress
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

Troubleshooting:
---------------
* If you didnt launch the vm using the core user you need to access pdoman this way:
```
sudo runuser -u core -- podman ps
sudo runuser -u core -- podman-compose -f /opt/.podman/docker-compose.yml ps
```

References:
------------
* https://podman.io/docs
* https://github.com/louislam/uptime-kuma