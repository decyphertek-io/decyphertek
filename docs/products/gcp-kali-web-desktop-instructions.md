Kali Linux is an open source Penetration testing platform based on debian. You can access Kali Linux 
from your web browser and begin to assess your environment.

Kali Linux Web Desktop Login:
------------------------------
* ssh into your server: 
```
sudo cat /home/kali/password.txt
```
* Go to your browser - https://ip-of-server:6080/vnc.html
* Login with your password retrieved in the previous step.
* Left side tab - Select full screen + see additonal options. 
* Note: By default there is no security tools installed , due to GCP approval policies. 
* Default Toolset: 
```
sudo apt install kali-linux-default
```
* Everything Toolset: 
```
sudo apt install kali-linux-everything
```
* Note: Avoid installing any of the desktop meta packages as it modifies grub and breaks the system. You already have xfc4 desktop.
* Note: If your desktop locks when logged into nvnc, you will need to create a kali password: 
```
sudo passwd kali 
```
* Optional: Update vnc password:
```
sudo su kali
cd ~ 
vnpasswd 
sudo systemctl daemon-reload 
sudo systemctl restart tigervnc
```
* Kali Linux Tools - https://www.kali.org/tools/

Troubleshooting:
-----------------
* Make sure you are accessing https://ip-of-server:6080/vnc.html
* Your password is found in the kali linux home directory:
```
sudo cat /home/kali/password.txt
```
* Forgot your password, you can change it. run form terminal:
```
sudo su kali
cd ~
vncpasswd 
sudo systemctl daemon-reload 
sudo systemctl restart tigervnc
```
* If noVNC is not working, run from terminal:
```
sudo systemctl restart novnc
```

Additonal Security Features:
----------------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and at 3am daily.

References:
------------
* https://www.kali.org/