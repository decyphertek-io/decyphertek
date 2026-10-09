AWS Basics
----------

If you're new to AWS and need a quick reference guide, this is a good place to start. [AWS Marketplace: Decyphertek ](https://aws.amazon.com/marketplace/seller-profile?id=851968a2-7d3c-4a0b-8c33-5351d91aaef1)

SSH Keys:
--------
* Create a key pair for secure SSH access to your EC2 instances.
* Docs: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/create-key-pairs.html
* AWS Console > EC2 > Network & Security > Key Pairs > Create Key Pair
* Name your key > Choose a type: RSA or ED25519 > Format: OpenSSH (.pem) or PuTTY (.ppk) > Save
* Permissions: If you use a .pem key on Linux or macOS, restrict the permissions first:
```
chmod 400 key-pair-name.pem
```
* Recommended remote access software:
    * Windows: MobaXterm
    * Linux: Remmina
    * macOS: Royal TSX
* EC2 Launch: Select your newly created key pair when launching your EC2 instance.
* Networking: Ensure SSH is allowed via the security group, UFW allows SSH, and you have public or VPN access.

EC2 Status Checks:
-----------------
* Docs: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-system-instance-status-check.html
* Checking the status of your instance can reveal issues with your server.
* AWS Console > EC2 > Instances > check the Status column.
* Status: Running / Stopped / Pending / Failed.
* If the status shows red (1/2) and failed, something is wrong with the instance. A reboot can sometimes resolve the issue.
* Troubleshoot: Select the instance > Actions > Monitor & Troubleshoot > Get Instance Screenshot.

AWS Health Dashboard:
--------------------
* Docs: https://docs.aws.amazon.com/health/latest/ug/aws-health-dashboard-status.html
* Find out if there are any issues in your region, outages, etc.
* AWS Console > AWS Health Dashboard.

EC2 Networking Topics:
--------------------
If you would like to learn more about networking related to EC2 instances, here are some quick links.

* Security Groups - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/working-with-security-groups.html
* VPC - https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html
* Route Tables - https://docs.aws.amazon.com/vpc/latest/userguide/WorkWithRouteTables.html
* Internet Gateway - https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html#Add_IGW_Attach_Gateway
* Transit Gateway - https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html
* Elastic IPs - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html
