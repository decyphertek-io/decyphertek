Arch Linux is a versatile and lightweight Linux distribution designed for advanced users who value simplicity and customization. When paired with noVNC, it provides users the ability to access a full desktop environment directly from a web browser, making it convenient for remote management. Arch prioritizes security with features such as the UFW (Uncomplicated Firewall) for robust host protection, CrowdSec for real-time intrusion prevention, and Auditd for comprehensive logging. Additionally, automated updates ensure that the system remains current and secure, allowing users to focus on their tasks without worrying about maintenance. [AWS Marketplace: Arch Linux Web Desktop ](https://aws.amazon.com/marketplace/pp/prodview-m33yk2ncmkkea?sr=0-1&ref_=beagle&applicationId=AWSMPContessa)


Instructions:
---------------------
* Arch Linux is an open source linux distro. You can access Arch Linux from your web browser.
* Arch Linux Web Desktop Login:
```
ssh into your server: ssh arch@ip-of-server
Run from Terminal to find your instance id - curl -s http://169.254.169.254/latest/meta-data/instance-id 
```
* Create a userpassword:
```
sudo passwd arch
```
* Go to your browser:
```
https://ip-of-server:6080/vnc.html 
Username: arch
Password: instanceid
# Left side tab - Select full screen + see additonal options.
```
Optional:
-----------
* Update vnc password: 
```
vnpasswd 
sudo systemctl daemon-reload 
sudo systemctl restart tigervnc
```

Troubleshooting:
----------------
* AWS Basics - https://decyphertek.readthedocs.io/en/latest/products/aws-basics/ 
* Make sure you are accessing https://ip-of-server:6080/vnc.html 
* Your password is your instance ID, from terminal run - curl -s http://169.254.169.254/latest/meta-data/instance-id 
* Forgot your password, you can change it. run form terminal - vncpasswd , sudo systemctl daemon-reload , sudo systemctl restart tigervnc
* If noVNC is not working, run from terminal - sudo systemctl restart novnc
* The xfce4 desktop sometimes requires login with arch password, make sure you have it set - sudo passwd arch

Additonal Security Features:
----------------------------
* Ossec Hids - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/ 
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/ 
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/ 
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/ 
* Automated Updates - Via script on reboot and at 3am.

References:
-------------
* https://archlinux.org/ 
