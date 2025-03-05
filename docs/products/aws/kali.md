Kali Linux is an open source Penetration testing platform based on debian. You can access Kali Linux from your web browser and begin to assess your environment. [AWS Marketplace: Kali Linux Web Desktop ](https://aws.amazon.com/marketplace/pp/prodview-tgyveez3mnqfq?sr=0-6&ref_=beagle&applicationId=AWSMPContessa)


Instructions:
-------------------
* Kali Linux Web Desktop Login:
* ssh into your server: 
```
ssh kali@ip-of-server
```
* Run from Terminal to find your instance id : 
```
cat password.txt
```
* Go to your browser: 
```
https://ip-of-server:6080/vnc.html 
```
* Login with your password found at /home/kali/password.txt
* Left side tab - Select full screen + see additonal options.
* Note: By defualt there is no security tools installed , due to AWS AMI apporval policies.
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
sudo passwd kali
```
* Optional: Update vnc password: 
```
vnpasswd 
sudo systemctl daemon-reload 
sudo systemctl restart tigervnc
sudo systemctl restart nonvnc
```
* Enjoy & read up on AWS Pentest Policies - https://aws.amazon.com/security/penetration-testing/ 
* Kali Linux Tools - https://www.kali.org/tools/ 

Troubleshooting:
----------------
* AWS Basics - https://decyphertek.readthedocs.io/en/latest/products/aws-basics/ 
* Make sure you are accessing https://ip-of-server:6080/vnc.html 
* Your password is you instance ID, from terminal run - curl -s http://169.254.169.254/latest/meta-data/instance-id 
* Forgot your password, you can change it. run form terminal:
```
 vncpasswd 
 sudo systemctl daemon-reload 
 sudo systemctl restart tigervnc
 sudo systemctl restart nonvc
```
* If noVNC is not working, run from terminal: 
```
sudo systemctl restart novnc
```

Security Features:
------------------
* Ossec Hids - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/ 
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/ 
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/ 
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/ 
* Automated Updates - Update script upon first boot and at 3am daily.

References:
-----------
* https://www.kali.org/ 
