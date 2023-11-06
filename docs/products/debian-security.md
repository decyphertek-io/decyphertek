
Decyphertek has secured your AWS AMI with one or more of the following open source software. Please reference the specific softare stack your server has. As a courteousy to AWS Subscribers this section can be used as a quick reference. [AWSMP: Decyphertek ](https://aws.amazon.com/marketplace/seller-profile?id=851968a2-7d3c-4a0b-8c33-5351d91aaef1)

Security Features
-----------------

* Crowdsec IPS - An open source Intrusion prevntion system , that maintains a global IP blacklist. 
* UFW Host Firewall - A host based firewall that adds an addtional layer of security to limit access to your server. 
* Unattended Upgrades - Provides automated security patching & upgrades via crontab at 3am UTC every morning. 
* Auditd Logging - Provides additional security logging based of security aduitd rules set. 
* Quad9 DNS - Secure encrypted DNS that also blocks malicious queries and domains by default. 
* Modsecurity WAF - A Web Application firewall that block known malicous attacks against NGINX. 

AWS Basics
-----------

* SSH Keys - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/create-key-pairs.html
1. AWS Console Login > EC2 > Network & Security > Key Pairs > Create Key Pairs
2. Name the keys > Choose : RSA or ED25519 > Format: Openssh = .pem / PuTTY = .ppk > Save the key
3. Permissions: If your use .pem on linux or Mac change permissions on key > $ chmod 400 key-pair-name.pem
4. Recommended: Remote access Software > Windows - Mobaxterm / Linux - Reminna / Mac - Royal TSK 
4. EC2 Launch: When you launch your ec2 instance , reference your newly created key . 
5. Networking: Make sure you allow ssh via security group , ufw allows ssh , and you have public or private vpn access. 

* EC2 Status Check - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-system-instance-status-check.html
* Checking the status of your instance can reveal if there is any issues with your server.
1. AWS Console Login > EC2  > Instances > Check Status Column
2. Staus : Running / Stopped / Pending / Failed 
3. If stauts is red 1/2 and failed , then there is something wrong with your instance, reboots can solve the issue sometimes. 
4. Troubelshoot: Select Instance > Actions > Monitor & Troubleshoot > Get Instance Screenshot .

* AWS Health Dashboard - https://docs.aws.amazon.com/health/latest/ug/aws-health-dashboard-status.html
* Find out if there is any issues in your region, outages , etc. 
1. AWS Console Login > AWS Health Dashboard 
    
* AWS EC2 / Networking Topics 
* If you would like to learn more about networking , related to Ec2 instances, here is some quick links. 
1. Security Groups - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/working-with-security-groups.html
2. VPC - https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html
3. Route Tables - https://docs.aws.amazon.com/vpc/latest/userguide/WorkWithRouteTables.html
4. Internet Gateway - https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html#Add_IGW_Attach_Gateway
5. Transit Gateway - https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html
6. Elastic IPS - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html

Crowdsec IPS
------------

* Crowdsec recently updated their repo and when updating Debian 11 based systems , it produces a crowdsec error. The way to fix this is to run the following:
$ curl -s https://packagecloud.io/install/repositories/crowdsec/crowdsec/script.deb.sh | sudo bash
$ sudo apt update
* I will be updating the base Debian 11 image, it may have an impact on past customers. 

https://decyphertek.readthedocs.io/en/latest/#Crowdsec/


UFW Host Firewall
-----------------

https://decyphertek.readthedocs.io/en/latest/#UFW/

Unattended Upgrades
-------------------

https://decyphertek.readthedocs.io/en/latest/#Unattended-Upgrades/

Auditd Logging
--------------

https://decyphertek.readthedocs.io/en/latest/#Auditd/

Quad9 DNS
----------

https://decyphertek.readthedocs.io/en/latest/#Quad9/

Modsecurity WAF 
----------------

https://decyphertek.readthedocs.io/en/latest/#Nginx/
    


