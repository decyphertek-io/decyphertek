AWS Basics
-----------

If your new to AWS and need a quick reference guide, this is a good place to start. [AWS Marketplace: Decyphertek ](https://aws.amazon.com/marketplace/seller-profile?id=851968a2-7d3c-4a0b-8c33-5351d91aaef1)

* SSH Keys - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/create-key-pairs.html
* AWS Console Login > EC2 > Network & Security > Key Pairs > Create Key Pairs
* Name the keys > Choose : RSA or ED25519 > Format: Openssh = .pem / PuTTY = .ppk > Save the key
* Permissions: If your use .pem on linux or Mac change permissions on key > $ chmod 400 key-pair-name.pem
* Recommended: Remote access Software > Windows - Mobaxterm / Linux - Reminna / Mac - Royal TSK 
* EC2 Launch: When you launch your ec2 instance , reference your newly created key . 
* Networking: Make sure you allow ssh via security group , ufw allows ssh , and you have public or private vpn access. 

* EC2 Status Check - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-system-instance-status-check.html 
* Checking the status of your instance can reveal if there is any issues with your server.
* AWS Console Login > EC2  > Instances > Check Status Column
* Staus : Running / Stopped / Pending / Failed 
* If stauts is red 1/2 and failed , then there is something wrong with your instance, reboots can solve the issue sometimes. 
* Troubleshoot: Select Instance > Actions > Monitor & Troubleshoot > Get Instance Screenshot .

* AWS Health Dashboard - https://docs.aws.amazon.com/health/latest/ug/aws-health-dashboard-status.html 
* Find out if there is any issues in your region, outages , etc. 
* AWS Console Login > AWS Health Dashboard 
    
* AWS EC2 / Networking Topics
* If you would like to learn more about networking , related to Ec2 instances, here is some quick links. 
* Security Groups - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/working-with-security-groups.html
* VPC - https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html
* Route Tables - https://docs.aws.amazon.com/vpc/latest/userguide/WorkWithRouteTables.html
* Internet Gateway - https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html#Add_IGW_Attach_Gateway
* Transit Gateway - https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html
* Elastic IPS - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html
