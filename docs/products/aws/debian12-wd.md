Debian 12 Linux is an open source linux distribution that is well trusted to do system administration , penetration testing, and general IT work. [AWS Marketplace: Debian 12 Web Desktop ](https://aws.amazon.com/marketplace/pp/prodview-lly7zq5e5xixy?sr=0-2&ref_=beagle&applicationId=AWSMPContessa)


Debian 12 Linux Web Desktop Login:
----------------------------------
* ssh into your server: ssh admin@ip-of-server
* Run from Terminal to find your instance id - curl -s http://169.254.169.254/latest/meta-data/instance-id
* Go to your browser - https://ip-of-server:6080/vnc.html
* Login with your instance id
* Left side tab - Select full screen + see additonal options.
* Note: Some applications require a sudo password and if your desktop locks. sudo passwd admin
* Optional: Update vnc password - vnpasswd  , sudo systemctl daemon-reload , sudo systemctl restart tigervnc
* Enjoy

Troubleshooting:
---------------
* AWS Basics - https://decyphertek.readthedocs.io/en/latest/products/aws-basics/
* Make sure you are accessing https://ip-of-server:6080/vnc.html
* Your password is you instance ID, from terminal run - curl -s http://169.254.169.254/latest/meta-data/instance-id
* Forgot your password, you can change it. run form terminal - vncpasswd , sudo systemctl daemon-reload , sudo systemctl restart tigervnc
* If noVNC is not working, run from terminal - sudo systemctl restart novnc

Security Features:
------------------
* Ossec Hids - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and at 3am daily.

References:
----------
* https://www.debian.org/download
* https://www.flatpak.org