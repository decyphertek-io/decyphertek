OpenVAS Vulnerability Scanner is an advanced, open-source security tool designed for comprehensive vulnerability assessment and management. 
It efficiently scans and identifies potential security weaknesses in network services and software systems. [GCP Marketplace: OpenVas ](https://console.cloud.google.com/marketplace/product/server-build-415714/openvas)

Note:
------
* Please be aware that it takes a few minutes for Openvas to be up and running.

SSH Into the server:
--------------------
* Utilize Google SSH Console or setup ssh keys or password.

OpenVAS GVM Login:
------------------

* ssh into your server.
* Password:
```
sudo cat /home/adminotaur/password.txt 
```
* Recommended: Update gvm feeds ( Takes a while ):
```
sudo gvm-feed-update
```
* Go to your browser - https://ip-of-server
* Login:
```
username: admin 
password: ( Output of password.txt in adminotaur directory)
```

OpenVas Basics:
---------------

* Dashboard: Check Feeds > Administration > Feed Status
* Dashboard: Create a new Target > Configuration > Target > Select - Top Left: Paper W/ Star > New Target > Enter IP or Cidr range > Choose your options
* Dashboard: Create a New Port List > Configuration > Port List > Select - Top Left: Paper W/ Star > New Port List 
* Dashboard: Quick Scan > Scans > Tasks > Select - Top Left: Paper W/ Star  > New Task > Select Target > Set to once > Start 
* Terminal: Update Password > sudo runuser -u _gvm -- gvmd --user=admin --new-password=decyphertek && sudo systemctl daemon-reload && sudo systemctl restart gvmd
* Terminal: Update Feeds > sudo gvm-feed-update
* Terminal: Add New user > sudo runuser -u _gvm -- gvmd --create-user=newuser --new-password=password
* Getting Started W/ Openvas GVM > https://www.youtube.com/watch?v=LGh2SetiKaY

Troubleshooting:
-----------------

* Check the status of GVM > sudo systemctl status gvmd
* Stop GVM > sudo gvm-stop -h
* Start FVM > sudo gvm-start -h

Additonal Security Features:
----------------------------

* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and daily.
* Nginx - https://nginx.org/en/docs/

References:
------------

https://openvas.org/
