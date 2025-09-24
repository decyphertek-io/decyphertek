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
* Go to your browser - https://ip-of-server
* Login:
```
username: admin 
password: ( Output of password.txt )
```

OpenVas Basics:
---------------
* Dashboard: Check Feeds > Administration > Feed Status
* Dashboard: Create a new Target > Configuration > Target > Select - Top Left: Paper W/plus > New Target > Enter IP  
  or Cidr range > Choose your options
* Dashboard: Create a New Port List > Configuration > Port List > Select - Top Left: Paper W/ Star > New Port List 
* Dashboard: Quick Scan > Scans > Tasks > Select - Top Left: Paper W/ Star  > New Task > Select Target > Set to once 
  > Start 
* Terminal - Update Password:
```
sudo runuser -u _gvm -- gvmd --user=admin --new-password=PASSWORD
sudo systemctl daemon-reload 
sudo systemctl restart gvmd
```
* Terminal - Update Feeds: ( Optional )
```
sudo greenbone-feed-sync --type all 
```
* Terminal: Add New user:
```
sudo runuser -u _gvm -- gvmd --create-user=newuser --new-password=PASSWORD
```
* Getting Started W/ Openvas GVM > https://www.youtube.com/watch?v=LGh2SetiKaY

Troubleshooting:
-----------------
* Check to see if all services are running correctly. 
```
sudo systemctl status gvmd gsad ospd-openvas redis-server postgresql nginx
```
* You can stop,start, and restart services if not working. 
```
sudo systemctl stop gvmd gsad ospd-openvas redis-server postgresql nginx
sudo systemctl start gvmd gsad ospd-openvas redis-server postgresql nginx
sudo systemctl restart gvmd gsad ospd-openvas redis-server postgresql nginx
```
* If you get this error from the web browser login:
```
The Greenbone Vulnerability Manager service is not responding. This could be due to system maintenance. Please try again later, check the system status, or contact your system administrator.

# Check for issues with the gvmd.service
sudo journalctl -xeu gvmd.service
```
* One first boot a system update occurs, so this can update openvas and make the DB outdated in some cases. 
* Check to see if you have an outdated Database:
```
sudo -u _gvm gvmd --get-scanners
# If you get this message.
Database is wrong version.
Your database is too old for this version of gvmd.
Please migrate to the current data model.
Use a command like this: gvmd --migrate

# Please run this command to fix it.
sudo systemctl stop gvmd gsad ospd-openvas
sudo -u _gvm gvmd --migrate
sudo systemctl start gvmd gsad ospd-openvas
sudo greenbone-feed-sync --type all 
```
* Optional: Update gvm feeds ( Takes a while ):
* This is done via crontab automatically every sunday.
```
sudo greenbone-feed-sync --type all 
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
