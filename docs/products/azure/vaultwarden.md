Vaultwarden is a lightweight, self-hosted password manager that provides a more resource-efficient alternative to the official Bitwarden server. It offers full compatibility with Bitwarden client applications, enabling users to manage their passwords securely across different platforms. Vaultwarden ensures strong encryption and security for user data. It is community-driven, customizable, and ideal for those seeking full control over their password management system. [Azure Marketplace: Vaultwarden ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/decyphertek.vaultwarden?tab=Overview)


Note:
------
* After 5/27/26 uses podman instead of docker and requires the core user .
* After 5/27/26 Portainer is no longer used.
* After 5/27/26 Fedora CoreOS is used instead of FlatCar Linux
* After 5/27/26 Caddy and Coraza Waf is used instead of nginx. 
* Please be aware that it takes a few minutes for Vaultwarden to be up and running.

SSH Into the server:
--------------------
* Please launch the VM with the core user.
* Utilize Azure SSH settings to set your ssh keys AND/OR Password to ssh in. 

Vaultwarden:
------------
* How to access Vaultwarden > https://ip-of-server
* Select create a new account and follow the Instructions.
* Optional: Enable MFA - Login > Account Settings > Security > Two Step Login > Select and enable your MFA.  

Podman: 
-------
* Podman is a daemonless, rootless container engine used to run Vaultwarden and Caddy securely.
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
podman logs vaultwarden
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

Security: ( After 5/27/26 )
---------
* Fedora CoreOS 
* Automatoic Updates
* SE Linux
* Auditd 
* Firewalld
* Podman Containers
* Caddy Reverse proxy
* Coraza WAF 

References:
------------
* https://podman.io/docs
* https://github.com/dani-garcia/vaultwarden


