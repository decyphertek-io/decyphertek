SonarQube is an open-source platform for continuous inspection of code quality, helping developers identify and fix bugs and vulnerabilities across multiple programming languages. It provides detailed reports on overall code health, ensuring high standards in software development. Running on Fedora CoreOS with Podman, your SonarQube instance benefits from a secure, containerized environment that simplifies deployment and scaling, with security features like an immutable OS, automatic updates, SELinux, and Caddy with Coraza WAF ensuring robust protection and stability. [Azure Marketplace: SonarQube CE](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/decyphertek.sonarqube-ce?tab=Overview)


Note:
------
* After 5/29/26 uses podman instead of docker and requires the core user.
* After 5/29/26 Fedora CoreOS is used instead of FlatCar Linux.
* After 5/29/26 Caddy and Coraza WAF is used instead of nginx.
* Please be aware that it takes a few minutes for SonarQube CE to be up and running.

SSH Into the server:
--------------------
* Please launch the VM with the core user.
* Utilize Azure SSH settings to set your ssh keys AND/OR Password to ssh in.

SonarQube CE:
-------------
* How to access SonarQube > https://ip-of-server
* It immediately requires updating password before you can login.
```
username: admin
password: admin
```

Podman:
-------
* Podman is a daemonless, rootless container engine used to run SonarQube and Caddy securely.
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
podman logs sonarqube
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

Security: ( After 5/29/26 )
---------
* Fedora CoreOS
* Automatic Updates
* SE Linux
* Auditd
* Firewalld
* Podman Containers
* Caddy Reverse proxy
* Coraza WAF

References:
-----------
* https://podman.io/docs
* https://docs.sonarsource.com/sonarqube/latest/