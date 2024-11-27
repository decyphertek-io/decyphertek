Rocky 9 Enterprise Linux is an open source linux distribution built as a one for one replacement for Red Hat 9 Enterprise and the End Of Life Centos. [Azure Marketplace: Rocky 9 Web Desktop ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/decyphertek.rocky9-web-desktop?tab=Overview)


SSH Into the server:
--------------------
* Utilize Azure SSH settings to set your ssh keys AND/OR Password to ssh in. 

Instructions:
-------------
* Run from Terminal to find your instance id :
```
sudo cat /root/password.txt
```
* Go to your browser: 
```
https://ip-of-server:6080/vnc.html 
```
* Login with your password.
* Left side tab - Select full screen + see additonal options.
* Note: Some applications require a password and if your desktop locks:
```
sudo su
passwd
```
* Optional: Update vnc password:
```
sudo su
cd ~
vnpasswd
systemctl daemon-reload 
systemctl restart vncserver@:1.service
systemctl restart nonvnc
```

Troubleshooting:
----------------
* Make sure you are accessing https://ip-of-server:6080/vnc.html 
* Your password is located at : /root/password.txt 
* Forgot your password, you can change it. run form terminal:
```
sudo su
cd ~
vnpasswd
systemctl daemon-reload 
systemctl restart vncserver@:1.service
systemctl restart nonvnc
```
* If noVNC is not working, debug any errors: 
```
sudo systemctl status vncserver@:1.service
sudo systemctl status nonvnc
```

Security Features:
------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/ 
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/ 
* Automated Updates - https://dnf.readthedocs.io/en/latest/automatic.html 
* Firewalld Host Firewall - https://firewalld.org/ 

References:
-----------
* https://rockylinux.org/ 