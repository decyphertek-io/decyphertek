Debian 12 Web Desktop utlizes noVNC to make Linux accessible from your web browser. Debian 12 Linux is an open source 
linux distribution that is well trusted to do system administration , penetration testing, and general IT work. 
[GCP Marketplace: Debian 12 Web Desktop ](https://console.cloud.google.com/marketplace/product/server-build-415714/debian-12-web-desktop)

Note:
-------
* Please be aware that it takes a few minutes for the system to be up and running. 

SSH Into the server:
--------------------
* Utilize Google SSH Console or setup ssh keys or password.

Debian 12 Web Desktop:
------------------------------
* Run from Terminal to find your login password:
```
sudo cat /home/adminotaur/password.txt
```
* Go to your browser:
```
https://ip-of-server:6080/vnc.html
```
* Login with your password found at /home/adminotaur/password.txt
* Left side tab - Select full screen + see additonal options. 
* Note: Some applications may require a sudo password and if your desktop locks, you may need to create a sudo password.
``` 
sudo passwd adminotaur
```
* To launch applications that require sudo in the application bar, edit and add.
```
sudo -E APPNAMEHERE
```
* Enjoy 

Troubleshooting:
-----------------
* Make sure you are accessing https://ip-of-server:6080/vnc.html
* Your password is located at /home/adminotaur/password.txt
* Forgot your password, you can change it. run form terminal:
```
sudo su adminotaur
cd ~
vncpasswd
sudo systemctl daemon-reload 
sudo systemctl restart tigervnc
sudo systemctl restart novnc
```
* Make sure you have firewall access and services are running:
```
sudo systemctl status tigervnc
sudo systemctl status novnc
sudo ufw status numbered
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
