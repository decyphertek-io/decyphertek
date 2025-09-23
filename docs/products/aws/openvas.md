The OpenVAS GVM Vulnerability Scanner is an advanced, open-source security tool designed for comprehensive vulnerability assessment and management. It efficiently scans and identifies potential security weaknesses in network services and software systems. [AWS Marketplace: Openvas ](https://aws.amazon.com/marketplace/pp/prodview-cu6eq35jv7tek?sr=0-3&ref_=beagle&applicationId=AWSMPContessa)


OpenVAS GVM Login:
------------------
* ssh into your server: 
```
ssh adminotaur@ip-of-server
```
* Run from Terminal:
```
cat password.txt
```
* Go to your browser:
```
https://ip-of-server
username: admin 
paswword: SSH > From Terminal > cat password.txt
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

Security Features:
---------------------------
* Ossec Hids - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Rsyslog - https://www.rsyslog.com/doc/index.html
* Automated Updates - Update script upon first boot and at 3am daily.

References:
------------
* https://openvas.org/