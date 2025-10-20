Kali Linux is an open source Penetration testing platform based on debian. You can access Kali Linux from your web browser and begin to test and secure your environment.[Azure Marketplace: Kali Linux Web Desktop ]()

Note:
-----
* Please be patient , it takes a few minutes for Kali Linux Web Desktop to be accessible. 

SSH Into the server:
--------------------
* Utilize Azure to setup user and ssh keys. 
* Make sure to allow ssh & port 6080 via network security group.

Kali Linux Web Desktop Login:
------------------------------
* ssh into your server: 
```
sudo cat /root/password.txt
```
* Go to your browser - https://ip-of-server:6080/vnc.html
* Login with your password retrieved in the previous step.
* Left side tab - Select full screen + see additonal options. 
* Note: By default there is no security tools installed , due to Azure approval policies. 
* Default Toolset: 
```
sudo apt install kali-linux-default
```
* Everything Toolset: 
```
sudo apt install kali-linux-everything
```
* Note: If your desktop locks when logged into nvnc, you will need to create a kali password: 
```
sudo passwd root
```
* Optional: Update vnc password:
```
sudo su 
cd ~ 
vnpasswd 
sudo systemctl daemon-reload 
sudo systemctl restart tigervnc
```
* Kali Linux Tools - https://www.kali.org/tools/

Troubleshooting:
-----------------
* Make sure you are accessing https://ip-of-server:6080/vnc.html
* Your password is found in the kali linux root directory:
```
sudo cat /root/password.txt
```
* Forgot your password, you can change it. run form terminal:
```
sudo su 
cd ~
vncpasswd 
sudo systemctl daemon-reload 
sudo systemctl restart tigervnc
```
* If noVNC is not working, run from terminal:
```
sudo systemctl restart novnc
```

Security Features:
------------------
* Auditd - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* OSSEC HIDS - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/
* UFW - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Rsyslog - https://www.rsyslog.com/doc/index.html
* Automated Updates - Crontab runs at first boot and at 3am every morning.
* Security Reports:
```
# Daily Security report
sudo cat /var/log/decyphertek/security_report*
```

References:
-----------
* https://www.kali.org/