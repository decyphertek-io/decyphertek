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
    - Top Right: Account > Account Settings > Change Password
    - Enter Old Password & New password > Save.

Network MTU Settings:
---------------------
* Change MTU to 1460 to be compatible with GCP.
    - Network > Interfaces & Devices > 
        - LAN > Edit > Advanced > MTU = 1460 > Reconfigure Interface
        - WAN > Edit > Advanced > MTU = 1460 > Reconfigure Interface
    - Click Unsaved Changes > Apply Changes

Security Hardening:
------------------
* Replace Default SSL Certificate:
    - https://docs.nethsecurity.org/en/latest/reverse_proxy.html
    - Generate self-signed certificate or import existing certificate
    - System > Certificates > Import Certificate
    - Set as default
    - Click Unsaved Changes > Apply Changes
    - Refresh Browser & Accept new cert warning ( If Self Signed )
```
# Generate Self Signed cert. Can run from firewall terminal and copy to your system. Then upload.
openssl req -x509 -nodes -days 3650 -newkey ec:<(openssl ecparam -name secp384r1) \
-keyout self-signed-key.pem \
-out self-signed-crt.pem \
-subj "/C=US/ST=Any/L=Anytown/O=decyphertek/OU=adminotaur/CN=decyphertek"
# After changing produces an error, copy command and run from terminal.
```
* If cert change unsuccesful, change back to original Cert. 
```
#To fix broken Web UI access, from terminal run:
echo '{"name":"_lan"}' | /usr/libexec/rpcd/ns.reverseproxy call set-default-certificate
```
* Disable Allow SSH Password auth:
    - system > ssh > Uncheck Allow SSH password authentication > Save & Apply

* Update System:
    - System > Updates > Check for Fixes

* System Updates:
    * Only required for a major verison Upgrade.
    * Proceed with caution, backup before proceeding.
    - System > Updates > System Updates
    - https://nethsecurity.org/download
    - Extract & Upload

* Create an Admin User:
    - Users & Objects > User Databases > Add User
        - Username: USERNAME
        - Display Name: USERNAME
        - User Password: PASSWORD
        - Administrator User: Enabled
        - Add User
        - Click Unsaved Changes > Apply Changes 

* Note: You can only ssh in as the root user, not the new admin user. 

* Serial Console Access:
    - If you are unable to access SSH Access, can access via serial console.
    - GCP > Instance > Edit > Enable Serial Console access
    - Connect to Serial Console > Enter > Login as root

* Enable Multi-Factor Authentication:
    - Security > Authentication > MFA
    - Enable MFA
    - Configure Authentication App
    - Scan QR code with Google Authenticator or similar app
    - Enter verification code to confirm
    - Save

Network Configuration:
----------------------
```
# If you want to access the LAN from the VPN you need to setup VPC Peering:
# From Google Cloud ( EX: decyphertek is just an example , use your own nomenclature)
```
* Create WAN to LAN VPC Peering:
   - GCP > VPC Network > VPC Network Peering > Create Connection
   - Name: wan-to-lan-peering
   - Your VPC: decyphertek-wan
   - Peered VPC: lan-decyphertek
   - Check all import/export route options
   - Click Create

* Create LAN to WAN VPC Peering:
   - GCP > VPC Network > VPC Network Peering > Create Connection
   - Name: lan-to-wan-peering
   - Your VPC: lan-decyphertek
   - Peered VPC: decyphertek-wan
   - Check all import/export route options
   - Click Create
```
# From Terminal
# NOTE: Your source and destination VM instances must have canIpForward enabled. 
# In my testing just enabling it on NethSecurity, I was allowed to ssh into a LAN instance. 
# If you forgot to enable it during launching NethSecurity. 
gcloud auth application-default login
gcloud compute instances describe opnsense | grep canIpForward
gcloud config list project
gcloud compute instances list --filter="name=YOUR_INSTANCE"
gcloud compute instances export YOUR_INSTANCE --project YOUR_PROJECT_ID --zone YOUR_ZONE --destination=config.txt
# EX: Can use your own text editor.
vim config.txt
canIpForward: true
esc + :wq!
gcloud compute instances update-from-file YOUR_INSTANCE --project YOUR_PROJECT_ID --zone YOUR_ZONE --source=config.txt --most-disruptive-allowed-action=REFRESH
gcloud compute instances describe YOUR_INSTANCE | grep canIpForward
# Should return : canIpForward: true
```

* GCP > VPC Network > Routes > Route Mangement > Create Route
   - Name: lan-to-openvpn
   - Description: Allows a LAN route to OpenVPN Subnet. 
   - Network: lan-decyphertek
   - Route Type: Static Route  
   - IP Version: IPv4
   - Destination IP range: 10.134.85.0/24
   - Next hop: Specify an Instance
   - Next hop Instance: nethsecurity
   - Priority: 900 


OpenVPN Road Warrior Setup:
---------------------------
* Setup OpenVPN Road Warrior:
    - VPN > OpenVPN > Create Server
    - Server Name: OpenVPN-Server
    - User Database: Local database
    - Create an account for each user: Optional
    - Authentication: Username + Passowrd + Certificate
    - Mode: Routed
    - VPN Network: 10.134.85.0/24
    - Save & Apply

* Create VPN Users:
    - System > Users > Create User
    - Can use existing users or create a new one. 
    - Username: vpnuser
    - Set password
    - Add to OpenVPN group
    - Save

* Add a VPN Account:
    - VPN > OpenVPN Road Warrrior > Add VPN Account:
        - User: Select your user
        - Reserve IP: Optional
        - Cert Expiration: 3650 ( 10 yrs. )
        - add account & apply

* Firewall Rules - Allow OpenVPN access via WAN:
    - Firewall > Rules > Input Rules > Add Input rules:
        - Rule Name: Allow-OpenVPN-from-WAN
        - Source Type: Any Source Address
        - Destination Service: openvpn
        - Action: Accept
        - Rule Position: Add to the Top.
        - Save & Apply

* Firewall Rules - Enable NAT for VPN clients:
    - Firewall > NAT > Add NAT Rule:
        - Rule Name: NAT-VPN-to-WAN
        - Source Zone: openvpn
        - Destination Zone: wan
        - Source Address: 10.134.85.0/24
        - Destination Address: Any
        - Translation: Masquerade
        - Rule Position: Add to the Top.
        - Save & Apply

* Zones & Policies:
    - The correct forward routes enabled by default.
    - LAN > RWOPENVPN 
    - RWOPENVPN > LAN

* Download Client certificate:
    - VPN > OpenVPN Road Warrior > VPN User > Click options next to edit:
        - Download Certificate 
    - Import to OpenVPN > Test VPn Connect & Routes. 
    
References:
-----------
* https://docs.nethsecurity.org/en/latest/
* https://cloud.google.com/vpc/docs/vpc-peering
