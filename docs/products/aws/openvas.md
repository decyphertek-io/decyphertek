The OpenVAS GVM Vulnerability Scanner is an advanced, open-source security tool designed for comprehensive vulnerability assessment and management. It efficiently scans and identifies potential security weaknesses in network services and software systems. [AWS Marketplace: Openvas ](https://aws.amazon.com/marketplace/pp/prodview-cu6eq35jv7tek?sr=0-3&ref_=beagle&applicationId=AWSMPContessa)


OpenVAS GVM Login:
------------------
* ssh into your server: ssh adminotaur@ip-of-server
* Run from Terminal:
```
cat password.txt
```
* Recommended: Update gvm feeds ( Takes a while ) :
```
sudo gvm-feed-update
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
* Dashboard: Create a new Target > Configuration > Target > Select - Top Left: Paper W/ Star > New Target > Enter IP or Cidr range > Choose your options
* Dashboard: Create a New Port List > Configuration > Port List > Select - Top Left: Paper W/ Star > New Port List 
* Dashboard: Quick Scan > Scans > Tasks > Select - Top Left: Paper W/ Star  > New Task > Select Target > Set to once > Start 
* Terminal: Update Password > sudo runuser -u _gvm -- gvmd --user=admin --new-password=decyphertek && sudo systemctl daemon-reload && sudo systemctl restart gvmd
* Terminal: Update Feeds > sudo gvm-feed-update
* Terminal: Add New user > sudo runuser -u _gvm -- gvmd --create-user=newuser --new-password=password
* Getting Started W/ Openvas GVM > https://www.youtube.com/watch?v=LGh2SetiKaY

Troubleshooting:
----------------
* AWS Basics - https://decyphertek.readthedocs.io/en/latest/products/aws-basics/
* Check the status of GVM :
```
sudo systemctl status gvmd
# Stop GVM 
sudo gvm-stop -h
# Start FVM 
sudo gvm-start -h

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