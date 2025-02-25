Parrot OS is an open source penetration testing platform based on Debian, designed for security professionals and developers. It provides a comprehensive suite of tools for vulnerability assessment, digital forensics, and privacy protection. Parrot OS can be accessed directly from your web browser via noVNC. [AWS Marketplace: ParrotOS Web Desktop ](https://aws.amazon.com/marketplace/pp/prodview-q5skrk5xt3jpy?sr=0-8&ref_=beagle&applicationId=AWSMPContessa)


ParrotOS Web Desktop Login:
---------------------------
* ssh into your server: ssh parrot@ip-of-server
* Run from Terminal to find your instance id:
```
curl -s http://169.254.169.254/latest/meta-data/instance-id 
```
* Go to your browser:
```
https://ip-of-server:6080/vnc.html 
```
* Login with your instance id
* Left side tab > Select full screen + see additonal options.
* Note: By default there is no security tools installed , due to AWS AMI approval policies.
* Everything Toolset: 
```
sudo apt update
sudo apt install parrot-tools-full
```
* Note: If your desktop locks when logged into nvnc, you will need to create a parrot password: 
```
sudo passwd parrot
```
* Optional: Update vnc password:
```
vnpasswd
sudo systemctl daemon-reload 
sudo systemctl restart tigervnc
```
* Enjoy & read up on AWS Pentest Policies - https://aws.amazon.com/security/penetration-testing/ 
* Parrot OS Tools DOC - https://www.parrotsec.org/docs/category/tools 

Troubleshooting:
---------------
* AWS Basics - https://decyphertek.readthedocs.io/en/latest/products/aws-basics/ 
* Make sure you are accessing:
```
https://ip-of-server:6080/vnc.html 
```
* Your password is you instance ID, from terminal run - curl -s http://169.254.169.254/latest/meta-data/instance-id 
* Forgot your password, you can change it. run form terminal:
```
vncpasswd
sudo systemctl daemon-reload
sudo systemctl restart tigervnc
```
* If noVNC is not working, run from terminal:
```
sudo systemctl restart novnc
```
* No public Key Error, unable to update:
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7A8286AF0E81EE4A
sudo mv /etc/apt/trusted.gpg /etc/apt/trusted.gpg.d/parrot.gpg
sudo apt update
```

Security Features:
-----------------
* Ossec Hids - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/ 
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/ 
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/ 
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/ 
* Automated Updates - Update script upon first boot and at 3am daily.

References:
------------
* https://www.parrotsec.org/ 
