NethSecurity CE UTM Firewall is a powerful, open-source network security platform designed for comprehensive protection and intuitive management. It provides robust firewall capabilities, secure VPN connections, and an easy-to-use interface to safeguard your network infrastructure. [GCP Marketplace: NethSecurity Firewall]()

Note:
-----
* Requires x2 Network Interfaces.
* Two VPCs, x2 subnets in each subnet.
* Subnets have to be in the same region.
* Requires VPC Peering & Routes to access LAN from VPN. 
* Attach network interfaces as: WAN-VPC-Subnet 1st & LAN-VPC-Subnet 2nd. 
* Enable IPForwarding. Attach SSH Keys to ssh in as root. 

Login:
------
* Attach SSH Keys: 
    - ssh -i gcp.pem root@IP-OF-SERVER
* Retrieve Password: 
    - cat admin_password.txt
* Login to the Web UI.
    - https://IP-OF-SERVER
    - Username: root
    - Password: ( admin_password.txt )
* Please change the password once you login.
    - Top RIght: Click Profile Icon.
    - Enter Old Password &  new password > save.

References:
-----------
https://docs.nethsecurity.org/en/latest/
https://cloud.google.com/vpc/docs/vpc-peering
