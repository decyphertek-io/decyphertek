NethSecurity CE UTM Firewall is a powerful, open-source network security platform designed for comprehensive protection and intuitive management. It provides robust firewall capabilities, secure VPN connections, and an easy-to-use interface to safeguard your network infrastructure. [GCP Marketplace: NethSecurity Firewall]()

Note:
-----
* Recommended VM: e2-standard-2 or larger. 
* Requires x2 Network Interfaces.
* Two VPCs: x1 subnet in each VPC & in the same region.
* Attach network interfaces: WAN-VPC-Subnet 1st & LAN-VPC-Subnet 2nd. 
* WAN-VPC-Subnet Should set external IP as static. 
* LAN-VPC-Subnet should have External IP addresses as None.
* Enable IPForwarding. Attach SSH Keys to ssh in as root. 
* Requires VPC Peering & Routes to access LAN from VPN. 

Login:
------
* Attach SSH Keys: 
    - Security > Manage Access > Add Item
    - SSH Key Format > ssh-rsa SSH-KEY.pub root
    - ssh -i SSH-KEY.pem root@IP-OF-SERVER
    - If using Putty or Mobaxterm: Convert pem key to PPK format. 
* Retrieve Randomly generated Password: 
    - cat admin_password.txt
* Login to the Web UI.
    - https://IP-OF-SERVER
    - Username: root
    - Password: ( admin_password.txt )
* Please change the password once you login.
    - Top Right: Click Profile Icon.
    - Enter Old Password & new password > save.

References:
-----------
https://docs.nethsecurity.org/en/latest/
https://cloud.google.com/vpc/docs/vpc-peering
