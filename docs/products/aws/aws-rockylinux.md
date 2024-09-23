Rocky 9 Enterprise Linux is an open source linux distribution built as a one for one replacement for Red Hat 9 Enterprise and the End Of Life Centos. [AWS Marketplace: Rocky Linux Web Desktop ](https://aws.amazon.com/marketplace/pp/prodview-njvuo3xxzua5c?sr=0-9&ref_=beagle&applicationId=AWSMPContessa)


Instructions:
-------------
* ssh into your server: 
```
ssh rocky@ip-of-server
```
* Run from Terminal to find your instance id :
```
curl -s http://169.254.169.254/latest/meta-data/instance-id 
```
* Go to your browser: 
```
https://ip-of-server:6080/vnc.html 
```
* Login with your instance id
* Left side tab - Select full screen + see additonal options.
* Note: Some applications require a sudo password and if your desktop locks:
```
sudo passwd rocky
```
* Optional: Update vnc password:
```
vnpasswd
sudo systemctl daemon-reload 
sudo systemctl restart tigervnc
```
* Note: Openscap self scan requires loading rl9 .
* Enjoy

Troubleshooting:
----------------
* AWS Basics - https://decyphertek.readthedocs.io/en/latest/products/aws-basics/ 
* Make sure you are accessing https://ip-of-server:6080/vnc.html 
* Your password is you instance ID, from terminal run - curl -s http://169.254.169.254/latest/meta-data/instance-id 
* Forgot your password, you can change it. run form terminal - vncpasswd , sudo systemctl daemon-reload , sudo systemctl restart tigervnc
* If noVNC is not working, run from terminal - sudo systemctl restart novnc

Security Features:
------------------
* Ossec Hids - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/ 
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/ 
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/ 
* Automated Updates - https://dnf.readthedocs.io/en/latest/automatic.html 
* Firewalld Host Firewall - https://firewalld.org/ 

References:
-----------
* https://rockylinux.org/ 
* https://www.flatpak.org 
