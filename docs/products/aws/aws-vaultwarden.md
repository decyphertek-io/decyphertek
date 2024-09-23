Vaultwarden is a self-hosted password manager that allows users to securely store and manage their passwords and sensitive information while retaining complete control over their data. It is an open-source alternative to Bitwarden, designed for easy deployment and management. With features such as end-to-end encryption, user management, and file sharing capabilities, Vaultwarden provides a robust solution for individuals and teams looking to enhance their data privacy without relying on third-party services. [AWS Marketplace: Vaultwarden ](https://aws.amazon.com/marketplace/pp/prodview-lw5oi2w6y3uyu?sr=0-1&ref_=beagle&applicationId=AWSMPContessa)

Usage instructions:
--------------------

* Please be aware that it takes a few minutes for the system to be up and running.
  The best way to check is to view the status check from the ec2 / instances / dashboard.
  If it says intializing, it is not ready yet.*

* How to ssh into your server > ssh core@ip-of-server
* How to access Portainer to manage your containers > https://ip-of-server:9443 
* Follow the instructions to create a new admin account.
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happenes you need to restart the container, ssh into the server, then run. > docker restart portainer
* Once logged into portainer, click get started and select local. You can manage docker from here.
```
How to access Vaultwarden > https://ip-of-server 
Select create a new account and follow the instructions:
Optional: Enable MFA - Login > Account Settings > Security > Two Step Login > Select and enable your MFA.
Optional: Troubleshooting - If for some reason the startup script didnt run on first boot, please enable startup and reboot.
Optional: Troubleshooting - sudo systemctl enable startup && sudo reboot
```

Additonal Security Features:
----------------------------
* Ossec Hids - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/ 
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/ 
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/ 
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/ 
* Automated Updates - Via script on reboot and at 3am.

References:
-----------
* https://docs.docker.com/ 
* https://www.flatcar.org/docs/latest 
* https://github.com/dani-garcia/vaultwarden 
