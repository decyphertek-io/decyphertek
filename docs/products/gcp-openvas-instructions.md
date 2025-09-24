OpenVAS Vulnerability Scanner is an advanced, open-source security tool designed for comprehensive vulnerability assessment and management. It efficiently scans and identifies potential security weaknesses in network services and software systems. [GCP Marketplace: OpenVas ](https://console.cloud.google.com/marketplace/product/server-build-415714/openvas)

Note:
------
* Please be aware that it takes a few minutes for Openvas to be up and running.

SSH Into the server:
--------------------
* Connect SSH > Utilize Google Cloud Shell ( SSH-in-browser ) 
* OR setup ssh keys > Edit > SSH Keys > Add item > ssh-rsa SSH PUB KEY adminotaur
```
# May take up to a minute or two to sync the changes. 
ssh adminotaur@IP-OF-SERVER
```
* If unable to use either ssh solutions, please review your permisisons in GCP.

OpenVAS GVM Login:
------------------
* ssh into your server.
* Password:
```
sudo cat /home/adminotaur/password.txt 
```
* Go to your browser - https://ip-of-server
* Login:
```
username: admin 
password: ( Output of password.txt )
```
* You may see feeds syncing or Error fetching the feed , please wait for feeds to update. 

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
sudo apt update && sudo apt upgrade -y 
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
* In rare cases Updates can break Google SSH In A Browser functionality. 
```
# The newest version addresses this issue. If you have an older version , you can fix it this way. 
sudo vim /etc/ssh/sshd_config.d/gcp-compatibility.conf

# Google Cloud Console SSH compatibility
KexAlgorithms diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1,curve25519-sha256,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha1,diffie-hellman-group14-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,diffie-hellman-group1-sha1

# Ensure compatibility ciphers are available
Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com,chacha20-poly1305@openssh.com,aes256-cbc,aes192-cbc,aes128-cbc

# MAC algorithms for compatibility
MACs umac-64-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-64@openssh.com,umac-128@openssh.com,hmac-sha2-256,hmac-sha2-512,hmac-sha1

sudo systemctl restart sshd
```

Additonal Security Features:
----------------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and daily.
* Nginx - https://nginx.org/en/docs/
* Daily Security Report: ( Scheduled via crontab )
```
cd /var/log/decyphertek/
ls
sudo cat security_report_DATE-HERE.log
```

References:
------------
* https://openvas.org/
