OpenVAS Vulnerability Scanner is an advanced, open-source security tool designed for comprehensive vulnerability assessment and management. 
It efficiently scans and identifies potential security weaknesses in network services and software systems. [Azure Marketplace: OpenVas ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/decyphertek.openvas?tab=Overview)


Note:
------
* Please be aware that it takes a few minutes for Openvas to be up and running.

SSH Into the server:
--------------------
* Utilize Azure to setup user and ssh keys. 
* Make sure to allow ssh, https via network security group.

OpenVAS GVM Login:
------------------

* ssh into your server.
* Password:
```
sudo cat /root/password.txt 
```
* Recommended: Update gvm feeds ( Takes a while ):
```
sudo greenbone-feed-sync
```
* Go to your browser - https://ip-of-server
* Login:
```
username: admin 
password: ( Output of password.txt )
```

OpenVas Basics:
---------------

* Dashboard: Check Feeds > Administration > Feed Status
* Dashboard: Create a new Target > Configuration > Target > Select - Top Left: Paper W/ Star > New Target > Enter IP or Cidr range > Choose your options
* Dashboard: Create a New Port List > Configuration > Port List > Select - Top Left: Paper W/ Star > New Port List 
* Dashboard: Quick Scan > Scans > Tasks > Select - Top Left: Paper W/ Star  > New Task > Select Target > Set to once > Start 
* Terminal: Update Password:
```
sudo runuser -u gvm -- gvmd --user=admin --new-password=password
sudo systemctl daemon-reload 
sudo systemctl restart gvmd
```
* Terminal: Update Feeds:
```
sudo greenbone-feed-sync
```
* Terminal: Add New user:
```
sudo runuser -u gvm -- gvmd --create-user=newuser --new-password=password
```
* Getting Started W/ Openvas GVM:
```
https://www.youtube.com/watch?v=LGh2SetiKaY
```

Troubleshooting:
-----------------
```
sudo systemctl status gsad.service gvmd.service ospd-openvas.service notus-scanner.service
```

Additonal Security Features:
----------------------------

* Crowdsec IPS - https://www.crowdsec.net/
* Firewalld - https://firewalld.org/
* Auditd Logging - https://linux.die.net/man/8/auditd
* Automated Updates - https://dnf.readthedocs.io/en/latest/automatic.html
* Nginx - https://nginx.org/en/docs/

References:
------------

* https://openvas.org/
* https://docs.greenbone.net/GSM-Manual/gos-22.04/en/web-interface.html
