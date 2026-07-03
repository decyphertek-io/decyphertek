MISP (Malware Information Sharing Platform & Threat Sharing) is an open-source platform designed to enhance cybersecurity by improving the sharing of structured threat information among organizations. MISP is typically used to bolster threat intelligence for SIEM systems or during the triage of security incidents. Running on Fedora CoreOS with Podman, your MISP instance benefits from a secure, containerized environment that simplifies deployment and scaling, with security features like an immutable OS, automatic updates, SELinux, and Caddy with Coraza WAF ensuring robust protection and stability. [Azure Marketplace: MISP](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/decyphertek.misp?tab=Overview)


Note:
------
* After 5/30/26 uses podman instead of docker and requires the core user.
* After 5/30/26 Portainer is no longer used.
* After 5/30/26 Fedora CoreOS is used instead of FlatCar Linux.
* After 7/2/26 The new podman path is /home/core/.podman/ , ~/opt/.podman/ is not longer used. 
* Please wait 5-10 minutes for MISP to be accessible.
* Upon first login the system may be undergoing an update and display a warning message. Please wait.

SSH Into the server:
--------------------
* Please launch the VM with the core user.
* Utilize Azure SSH settings to set your ssh keys AND/OR Password to ssh in.

MISP - Access The Server:
-------------------------
* How to access MISP > https://ip-of-server
* Retrieve the admin password — ssh into the server then run:
```
cat /var/home/core/.podman/.env | grep ADMIN_PASSWORD
```
* Login credentials:
```
Username: admin@misp
Password: (retrieved from command above)
```
* Get data feeds > Dashboard > Sync Actions > Feeds > Load Default feed metadata > select pencil indicator, enable, submit > Fetch & store all Feed Data
* Change Password > Dashboard > Administration > List users > select user > Set Password > Save: Edit User - Confirm with old password

Podman:
-------
* Podman is a daemonless, rootless container engine used to run MISP and Caddy securely.
* Check running containers:
```
podman ps
```
* Update containers — ssh into the server then run:
```
cd /home/core/.podman/
podman-compose down
podman-compose pull
podman-compose up -d
```
* View container logs:
```
podman logs nginx-reverse-proxy
podman logs misp-core
podman logs misp-modules
podman logs mariadb
podman logs redis
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
* If you didnt launch the vm using the core user you need to access podman this way:
```
sudo runuser -u core -- podman ps
sudo runuser -u core -- podman-compose -f /opt/.podman/docker-compose.yml ps
```
* If IP changes or no Public IP — edit the .env file:
```
vi /home/core/.podman/.env
    BASE_URL=https://your-server-IP
cd /home/core/.podman/
podman-compose down
podman-compose up -d
```
* Check for SeLinux blocks and solutions:
```
sudo sealert -a /var/log/audit/audit.log
```

Security: ( After 5/30/26 )
---------
* Fedora CoreOS 
* Automatic Updates
* Podman Containers
* Firewalld
* SE Linux
* Auditd 
* Nginx

References:
-----------
* https://podman.io/docs
* https://www.misp-project.org/
* https://github.com/MISP/misp-docker
