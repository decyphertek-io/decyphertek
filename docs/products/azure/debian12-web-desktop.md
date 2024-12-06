Debian 12 Web Desktop utlizes noVNC to make Linux accessible from your web browser. Debian 12 Linux is an open source 
linux distribution that is well trusted to do system administration , penetration testing, and general IT work. 
[Azure Marketplace: Debian 12 Web Desktop ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/decyphertek.debian12-web-desktop?tab=Overview)


SSH Into the server:
--------------------
* Utilize Azure SSH settings to set your ssh keys AND/OR Password to ssh in. 

Debian 12 Web Desktop:
------------------------------
* Run from Terminal to find your login password:
```
sudo cat /root/password.txt
```
* Go to your browser:
```
https://ip-of-server:6080/vnc.html
```
* Login with your password found at /root/password.txt
* Left side tab - Select full screen + see additonal options. 
* Note: Some applications may require a sudo password and if your desktop locks, you may need to create a sudo password.
``` 
sudo passwd root
```
* Enjoy 

Troubleshooting:
-----------------
* Make sure you are accessing https://ip-of-server:6080/vnc.html
* Your password is located at /root/password.txt
* Forgot your password, you can change it. run form terminal:
```
sudo su
cd ~
vncpasswd
systemctl daemon-reload 
systemctl restart tigervnc
systemctl restart novnc
```
* Make sure you have firewall access and services are running:
```
sudo systemctl status tigervnc
sudo systemctl status novnc
sudo ufw status numbered
```
* Flatpaks require --no-sandbox , since its being run as root. EX:
```
/usr/bin/flatpak run com.vscodium.codium run --no-sandbox
```

Additonal Security Features:
----------------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and at 3am daily.

References:
------------
* https://www.debian.org/download
* https://www.flatpak.org
