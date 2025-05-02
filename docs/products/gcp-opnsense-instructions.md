OPNsense® Firewall/Router/VPN/IDPS is a powerful, open-source network security platform designed for comprehensive protection and management. It provides robust firewall capabilities, secure VPN connections, and advanced intrusion detection and prevention systems to safeguard your network infrastructure. [GCP Marketplace: OPNsense](https://console.cloud.google.com/marketplace/product/server-build-415714/opnsense)

Note:
-----
* Two Network Interfaces are required.
* Serial Console Access is required.
* Can securely access OPNsense from your account via Serial Console.
* root doesnt have an inital password set. Requires setup. I have verbose instructions.
* Please be patient and follow the instructions. 

Google VPC and Netwrok Interafce setup:
---------------------------------------
When using multiple network interfaces from an instance, each interface must attach to a subnet that is in a 
different VPC network. You can't attach multiple network interfaces to the same subnet or to subnets that are 
in the same VPC network.

# Note: Subnets must be in the same region. 
* VPC Network > Create VPC Network > WAN-VPC & LAN-VPC ( OR use exisitng ones ) > create two subnets in the same region on both VPCs with different IP ranges. 
* Enable Global Routing if you are communicating across multiple regions which uses Cloud VPN or Cloud Interconnect.
* Note: select autosubnets will create 40+ subnets automaticly , custom subnets will not. 
* Please use a different IP range for each subnet in each seperate VPC to avoid IP conflicts in the firewall. 
* Also select Private Google Access for the LAN VPC to avoid it attaching public IPS. 
* Optional: Hybrid Subnets allow you to communicate to an on premise subnet. 
* When adding LAN, attached as the second network interface set external IP address to none. 

Remote Access:
--------------
* Please enable Serial Console > Launch VM > Click on VM > Edit > enable Remote Access: Enable connecting to serial ports > save
```
# In some cases this feature may be disable, to enable it from gcloud , run the following command with the right permissions:
gcloud resource-manager org-policies disable-enforce compute.disableSerialPortAccess --project=PROJECT NAME HERE
```
* Select VM > Under Details > Click : Connect To Serial Console
```
# When screen shows up click enter, login should show. 
Login: root 
# Password is empty , hit enter
Password:
```
* Once in the serial console as root, there should be an opnsense-shell menu
* Select option 8: Enter the shell to enable the root account to access the OPNsense Web Dashboard:
```
Enter an option: 8
# ( Make sure to copy the entire command from sed > config.xml >>> )
root@OPNsense:~ # sed -i '' 's/<disabled>1<\/disabled>/<disabled>0<\/disabled>/' /conf/config.xml
root@OPNsense:~ # exit
```
* Select Option 3: Reset the root password 
```
Enter an option: 3

The root user login behaviour will be restored to its defaults.

Do you want to proceed? [y/N]: Y

Type a new password: 
Confirm new password: 

The root user has been reset successfully.
```
* ( Keep the Serial console open , we be utilizing the Web UI and the Serial console. ) 
* You can now visit your IP address and login to the OPNsense Web Dashboard.
```
# Can use Internal or External IP:
# Accept Cert Warning
https://IP-OF-SERVER
Username: root
Password: What you set in option 3.
```
* We need to set a firewall rule that allows WAN access before we enable the LAN feature.
```
# Enable firewall so LAN can be enabled.
* Firewall > Rules > WAN > Add ( Red + Button ) :
# Change the following ( Can also utilized Google Firewall to whitelist access to Web UI as well. )
* Action = Pass
* Protocol = TCP 
* Source = Single Host or Network ( Select ANY if you do not want to whitelist access )
  # EX: Add your IP ( Be Aware that ISPs can change your IP , may need to set a range via /24 )
  155.18.184.119/32
* Destination = This Firewall
* Destination Port Range = HTTPS > HTTPS 
* Category = WAN
* Description = Firewall Web UI Admin Access 
* Save 
* Apply Changes 

# Enable LAN vtnet1
* Interfaces > Assignment :
* Device = vtnet1
* Description = LAN 
* Add 
* Save 
```
* Now lets go back to the serial console to finish setting up the WAN & LAN. 
* Select Option 1: Assign Network Interfaces
```
Enter an option: 1

Do you want to configure LAGGs now? [y/N]: N
Do you want to configure VLANs now? [y/N]: N

Valid interfaces are:

vtnet0           xx:xx:xx:xx:xx:xx VirtIO Networking Adapter
vtnet1           xx:xx:xx:xx:xx:xx VirtIO Networking Adapter

If you do not know the names of your interfaces, you may choose to use
auto-detection. In that case, disconnect all interfaces now before
hitting 'a' to initiate auto detection.

Enter the WAN interface name or 'a' for auto-detection: vtnet0

Enter the LAN interface name or 'a' for auto-detection
NOTE: this enables full Firewalling/NAT mode.
(or nothing if finished): vtnet1

Enter the Optional interface 1 name or 'a' for auto-detection
(or nothing if finished): 

The interfaces will be assigned as follows:

WAN  -> vtnet0
LAN  -> vtnet1

Do you want to proceed? [y/N]: Y
```
* Select Option 2: Set interface IP address ( Configure WAN )
```
Enter an option: 2

Available interfaces:

1 - LAN (vtnet1 - static, track6)
2 - WAN (vtnet0 - dhcp, dhcp6)

Enter the number of the interface to configure: 2

Configure IPv4 address WAN interface via DHCP? [Y/n] Y

Configure IPv6 address WAN interface via DHCP6? [Y/n] Y

Do you want to change the web GUI protocol from HTTPS to HTTP? [y/N] N
Do you want to generate a new self-signed web GUI certificate? [y/N] Y
Restore web GUI access defaults? [y/N] N
```
* Select Option 2: Set interface IP address ( Configure LAN )
```
Enter an option: 2

Available interfaces:

1 - LAN (vtnet1 - static, track6)
2 - WAN (vtnet0 - dhcp, dhcp6)

Enter the number of the interface to configure: 1

Configure IPv4 address WAN interface via DHCP? [Y/n] Y

Configure IPv6 address WAN interface via DHCP6? [Y/n] Y

Do you want to change the web GUI protocol from HTTPS to HTTP? [y/N] N
Do you want to generate a new self-signed web GUI certificate? [y/N] Y
Restore web GUI access defaults? [y/N] N
```
* You can now log out of the serial console:
```
Enter an Option: 0
```
* Go back to the Web UI and set the MTU on the LAN & WAN ( Google requires 1460 )
```
Login > Dashboard > Interfaces > LAN :
* MTU = 1460 
* Save
Interfaces > WAN :
* MTU = 1460 
* Save
* Apply Changes 
```

Enable MFA:
-----------
```
* Proceed With CAUTION!! This can lock you out of the Webgui and the Serial Console, if done incorrectly. Please test.
* To be safe , you can create a second Admin user to make sure your not locked out of the WebGUI & Can revert changes. 
* Create a Local MFA Server: 
- System > Servers > Add > Description = MFA > Type = Local + Timebased One Time Password > Save 
* Generate USER OTP: 
- System > Access > Users > Edit > OTP Feed > Select Gear ICOn > Save OTP via QR Code or plain Text Code.
* Test MFA Access: 
- System > Tester > Select : Authentication Server = MFA > Enter username > Password = OTP CODE + Password ( EX:123pass )
* Enable MFA Server: 
- System > Settings > Administration > Scroll down to Authetnication > Server = MFA > Save 
* Offical Test: 
- Logout > Login again > username > Password: OTP+Password ( EX: 123pass )
* When MFA is enable, the serial console requires the same password structure :
- Password: OTP+Password ( EX: 123pass )
```

Optional > Wizard:
----------------
* CAUTION: Changing some Web UI HTTPS settings can break access. Please see Troubleshooting section to fix. 
* To customize your settings with help from the Wizard.
* System > Wizard > next > Choose your desired Settings.

Optional > Enable SSH Access:
-----------------------------
* Enable SSH : System > Settings > Secure Shell > Click Enable Secure Shell > If Using the root user click Permit root user login > save
* Add SSH Keys: System > Access > Users > Edit User > Login Shell = /bin/csh > authorized keys ( .pub ) = rsa SSHKEY NAME > save 
```
# If you need to generate an ssh key, Linux Example:
ssh-keygen -t rsa -b 4096
# To SSH In: ( root example )
ssh -i keyname.pem root@IP-OF-SERVER
# To OPNsense shell menu can only be luanched as root:
# Bypass would be to add a dedicated admin to the wheel group, sudoers, and run sudo su. See next section.
opnsense-shell
```

Optional > Dedicated Admin User, no root:
---------------------------------------
* Create a new admin User: System > Access > Users > ADD New USER
```
# Example
Username: adminotaur
Password: DecyphertekPASSWORD!
Full Name: System Administrator
Login shell: /bin/sh
Group membership: admins
Privilges: Privileges
OTP Seed: Show > Select Gear icon > Generates a new OTP Code > Save
Authorized Keys: rsa SSHKEY NAME
> SAVE
```
* Test Login : System > Tester > Select : Authentocation Server = MFA > Enter username > Password = OTP CODE + Password ( EX:123pass )
* Test SSH: ssh -i keyname.pem adminotaur@IP-OF-SERVER
* Enter root serial console > Select option 8 shell OR ssh in as root:
```
# Run this command to add user to the wheel group
pw usermod adminotaur -G wheel
# Run this command to add to the sudoers
visudo
# Add below the similar root account
adminotaur ALL=(ALL) ALL
```
* Now test console access, once logged in run:
```
# This is bring up the interactive menu for the dedicated admin user.
sudo su
opnsense-shell
```
* Disable the root user: system > Access > users > Edit root > Check the Disabled box > Save

SSL VPN Road Warrior Setup:
--------------------------
```
# OPNsense OpenVPN Docs
* https://docs.opnsense.org/manual/how-tos/sslvpn_client.html

# If you want to access the LAN from the VPN you need to setup VPC Peering:
# From Google Cloud ( EX: decyphertek is just an example , use your own nomenclature)
* Create First VPC Peering:
   - VPC Network > VPC Network Peering > Create Connection
   - Name: wan-to-lan-peering
   - Your VPC: decyphertek-wan
   - Peered VPC: lan-decyphertek
   - Check all import/export route options
   - Click Create

* Create Second VPC Peering:
   - VPC Network > VPC Network Peering > Create Connection
   - Name: lan-to-wan-peering
   - Your VPC: lan-decyphertek
   - Peered VPC: decyphertek-wan
   - Check all import/export route options
   - Click Create

# From OPNsense Firewall
# May need to create multiple groups if you want specific access for different users.
# You can also utilize an exisitng user and add them to multiple groups. 
* Create VPN Group:
   - System > Access > Groups > Add (Red + Button):
      - Group Name: OpenVPN_Users
      - Description: OPNsense OpenVPN Users ACL
      - Privileges: Select privilges for user group
      - Members: Can add user to group when making VPN User.
      - Save

* Create VPN User:
   - System > Access > Users > Red + Button:
      - Username: USERNAME
      - Password: PASSWORD
      - Full Name: NAME
      - E-mail: EMAIL
      - Comment: OpenVPN user
      - Group Membership: OpenVPN_Users
      - Optional: The rest is optional
      - Save

* Add TOTP (Optional): ( See Enable MFA Section for verbose Instructions. ) 

* Create a Trust Authority
   - System > Trust > Authorities > Add (Red + Button)
      - Method: Create an internal Certificate Authority
      - Description: OPNsense-OpenVPN-CA
      - Key Type: RSA-2048
      - Digest Algorithm: SHA256
      - Issuer: Self-Signed
      - Lifetime: 3650 (10 yrs.)
      - County Code: YOUR COUNTRY 
      - State or Province: Your state or Province
      - City: Your city 
      - Organization: Your company name
      - Organizational Unit: IT
      - Email Address: admin@yourdomain.com
      - Common Name: Domain Name or IP of Server
      - OCSP uri: Leave Blank
      - Output: Leave Blank, autogenerated
      - Save 

* Create a Server Trust Certificate
   - System > Trust > Certificates > Add (Red + Button)
      - Method: Create an internal Certificate
      - Description: OPNsense-OpenVPN-Server-Cert
      - Type: Server Certificate
      - Private Key Location: Save On This Firewall
      - Key Type: RSA 2048 
      - Digest Algorithm: SHA-256
      - Issuer: OPNsense-OpenVPN-CA
      - Lifetime: 3650 (10 yrs.)
      - County Code: YOUR COUNTRY 
      - State or Province: Your state or Province
      - City: Your city 
      - Organization: Your company name
      - Organizational Unit: IT
      - Email Address: admin@yourdomain.com
      - Common Name: Domain Name or IP of Server
      - OCSP uri: Leave Blank
      - Alternative Names:
         - DNS Domain Names: Leave Blank if using just IP
         - IP Addresses: Your public IP of the VPN
         - URIS: Leave Blank
         - Email Addresses: leave Blank
      - Output: Leave Blank, autogenerated
      - Save 

* Create a Client Trust Certificate
  - System > Trust > Certificates > Add (Red + Button)
      - Method: Create an internal Certificate
      - Description: USERNAME-OpenVPN-Client-Cert
      - Type: Client Certificate 
      - Private Key Location: Save On This Firewall
      - Key Type: RSA 2048
      - Digest Algorithm: SHA-256
      - Issuer: OPNsense-OpenVPN-CA
      - Lifetime: 3650 (10 yrs.)
      - Country Code: Same as CA certificate
      - State/Province: Same as CA certificate
      - City: Same as CA certificate
      - Organization: Same as CA certificate
      - Organizational Unit: Same as CA certificate
      - Email Address: User's email address
      - Common Name: USERNAME
      - OCSP uri: Leave Blank
      - Alternative Names: Leave all blank
      - Output: Leave Blank, autogenerated
      - Save

* Configure OpenVPN:
   - VPN > OpenVPN > Instances > Add (Red + Button):
      - Role: Server 
      - Description: OpenVPN-Server 
      - Enabled: Check to Enable
      - Protocol: UDP ( TCP More Secure , except slower )
      - Port number: 1194 
      - Bind address: Leave blank 
      - Type: tun 
      - Server (IPv4): 10.10.0.0/24 (choose a subnet that doesn't conflict with LAN)
      - Server (IPv6): Leave blank (unless IPv6 support needed)
      - Topology: subnet 
      - Certificate: OPNsense-OpenVPN-Server-Cert
      - Verify Remote Certificate: Check this box
      - Certificate Revocation List: Leave blank
      - Verify Client Certificate: Required
      - Use OCSP: Leave unchecked
      - Certificate Depth: One (Client+Server)
      - TLS static key: None
      - Authentication: Local Database
      - Enforce local group: OpenVPN_Users
      - Strict User/CN Matching: No
      - Renegotiate time: 3600
      - Auth Token Lifetime: 0 (never expires) or 86400 (1 day)
      - Local Network: LAN subnet (EX: 10.0.1.0/24) ( See the LAN you attached )
      - Remote Network: Leave blank
      - Misc.
         - Options: Optional
         - Push Options: Optional
         - Redirect gateway: Optional
         - Register DNS: Check this box (helps Windows clients)
         - DNS Default Domain: Your domain OR (EX: localdomain)
         - DNS Servers: LAN DNS gateway (EX: 10.0.1.1) or 8.8.8.8
         - NTP Servers: Optional
      - Save & Apply

* Add WAN Firewall Rule For OpenVPN:
   - Firewall > Rules > WAN > Add (Red + Button):
      - Action: Pass
      - Interface: WAN
      - Direction: In
      - TCP/IP Version: IPv4
      - Protocol: UDP ( OR TCP if you set that previously)
      - Source: Any
      - Destination: WAN Address
      - Destination Port Range: (Other) 1194 > 1194
      - Category: VPN
      - Description: Allow OpenVPN Access
      - Save & Apply Changes

* Add OpenVPN Firewall Rule to Access LAN:
   - Firewall > Rules > OpenVPN > Add (Red + Button):
      - Action: Pass
      - Interface: OpenVPN
      - Direciton: In
      - TCP/IP Version: IPv4
      - Protocol: Any
      - Source: Any 
      # Set Destinatin to Any If You want to pass all traffic thorugh the VPN
      # For a split tunnel setup , where you only access LAN, Google Subnet, then.
      - Destination: Single Host or Network ( EX: 10.0.1.0/24 > your LAN network)
      - Category: VPN
      - Description: Allow VPN clients to access LAN ( OR VPN Internet Access )
      - Save & Apply Changes

* Add  LAN Interface Firewall Rules:
   - Firewall > Rules > LAN > Add (Red + Button):
     - Action: Pass
     - Interface: LAN
     - Protocol: Any
     - Source: OpenVPN net
     - Destination: LAN net
     - Category: LAN
     - Description: Allow VPN clients to LAN
     - Save & Apply Changes

* Enable NAT for VPN clients (Required if you want clients to access the internet through the VPN):
   - Firewall > NAT > Outbound
      - Mode: Select "Hybrid outbound NAT rule generation" or "Manual outbound NAT rule generation"
      - Save 
      - Click "Add" (Red + Button)
      - Interface: WAN
      - Protocol: any
      - Source Address: OpenVPN Net
      - Source port: any
      - Destination: any
      - Destination port: any
      - Translation / target: Interface address
      - Category: NAT
      - Description: OpenVPN clients outbound NAT
      - Save & Apply Changes

* Export Client Configuration:
   - VPN > OpenVPN > Client Export
   - Remote Access Server: OpenVPN-Server udp:1194
   - Export Type: File Type
   - Hostname: public IP or domain
   - Port: 1194
   - Use Random Local Port: Checked 
   - P12 Password/confirm: Optional
   - Validate server subject: Checked
   - Windows Certificate System Store: If Using Windows Check
   - Disable password save: Optional
   - Accounts / certificates: Download USERNAME-OpenVPN-Client-Cert

* OpenVPN Client App:
* https://openvpn.net/client/
   - Windows: Run the downloaded installer (.exe file)
   - Android/iOS: 
     - Install OpenVPN Connect app from app store
     - Import profile by scanning QR code or importing .ovpn file
   - macOS/Linux: 
     - Install OpenVPN client software 
     - Import the .ovpn configuration file

* Connect to VPN:
   - Launch OpenVPN client on device
   - Select the imported profile
   - Enter username and password when prompted
   - If TOTP is enabled, enter password + TOTP code
   - Wait for connection to establish

* Verify Connection:
   - VPN > OpenVPN > Connection Status
   - Check that client appears in the connected clients list
   - Verify client received proper IP address
   - Test connectivity to resources on your LAN

* Troubleshoot:
  - Verify OpenVPN port is open:
  - sudo nmap -Pn -sU -p 1194 PUBLIC-IP
  - Check Firewall Logs:
      - Firewall > Log Files > Live View
  - Check OpenVPN Logs:
      - VPN > openVPN > Log File
```

WireGuard Road Warrior Setup:
----------------------------
```
# https://docs.opnsense.org/manual/how-tos/wireguard-client.html
* Create the WireGuard server on OPNsense
- VPN > WireGuard > Instances > Add ( Red + Button ) :
  - Name: WireguardVPN
  - Generate keys with cogwheel icon
  - Listen Port: 51820
  # Make sure its different than the WAN & LAN Subnet CIDR Ranges.
  - Tunnel Address: 10.10.10.1/24

* Use the peer generator to create a Client Peer
- VPN > WireGuard > Peer Generator :
  - Instance: WiregaurdVPN
  - Endpoint: WAN-PUBLIC-IP:51820
  - Name: clientpeer
  - PublicKey: Autogenerated
  - PrivateKey: Autogenerated
  - Address: Autogenerated
  # If you want all traffic to pass through the VPN, then keep the default 0.0.0.0/0,::/0
  # EX: This allows all private IP traffic.
  - Allowed IPS: 10.10.10.0/24, 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16
  - Keep Alive: 27 
  - ( Copy and save the config locally as clientpeer.conf )
  - Select Apply 

* Unblock WAN Private & Bogon Networks
   - Interfaces > WAN
   - UNCHECK "Block private networks"
   - UNCHECK "Block bogon networks"
   - Save and Apply changes

* Interface assignment:
   - Interfaces > Assignments
   - Select wg0 from dropdown, add description
   - Click Red + to add it, then Save
   - Click on new interface under Interfaces menu
      - Enable interface, Checkbox
      - Set IPv4/IPv6 Configuration Type to None
   - Save and Apply changes

* MSS Clamping (normalization rules):
   - Firewall > Settings > Normalization
   - Click Red + Button to add a new rule.
      - Interface: Wireguard Group
      - Direction: Any, Protocol: any
      - Source/Destination: any
      - Description: Wireguard Normalization
      - Max MSS: 1380 (40 bytes less than WireGuard MTU)
   - Save & Apply changes

# WireGuard Firewll Rules
* Create RFC1918 Networks Alias:
   - Firewall > Aliases > IP
   - Click Add (Red + button)
   - Enabled : Checked
   - Name: RFC1918_Networks
   - Type: Network(s)
   - Categories: VPN
   # Press Enter after adding each IP range. It will produce an error if you add them all together as one.
   - Content: 192.168.0.0/16 10.0.0.0/8 172.16.0.0/12
   - Statistics: Optional
   - Description: Private IP ranges
   - Save

* Create WAN Firewall Rule (allows VPN connections):
   - Firewall > Rules > WAN
   - Click Add (Red + button )
   - Action: Pass
   - Protocol: UDP
   - Source: Any
   - Destination: WAN address
   - Destination port: (other) 51820
   - Log: Optional
   - Category: VPN
   - Description: Allow WireGuard VPN
   - Save
   - Apply Changes

* Allows VPN to access LAN:
   - Firewall > Rules > WireGuardVPN
   - Click Add (Red + button)
   - Action: Pass
   - Protocol: Any
   - Source: Any
   - Destination: RFC1918_Networks,LAN net
   - Category: LAN
   - Description: Allow VPN to LAN
   - Save
   - Apply Changes

* Allows VPN IP Internal Traffic:
   - Go to Firewall > Rules > WireGuardVPN
   - Edit the existing rule or add a new one:
   - Action: Pass
   - Protocol: Any
   - Source: Any
   - Destination: single host or network 10.10.10.0/24
   - Description: Allow WireGuard internal traffic
   - Save
   - Apply Changes
```
* Make sure you install wireguard-tools 
- wireguard-tools - https://www.wireguard.com/install/

* Troubleshooting : ( From a Linux System )
```
# Unable to access? Lets verify your not being blocked by a network or OPNsense firewall
sudo nmap -Pn -sU -p 51820 PUBLIC-IP
# Make sure you clientpeer.conf is correct EX:

[Interface]
PrivateKey = 2Bfxxu+u8xx8qR/5sBtwQAxxPx7f5dexxbl4=
Address = 10.10.10.2/32

[Peer]
PublicKey = xx+o3i0xx2HsoTeJ/TmvFwxxKX8mxxm/51Z92g58xxhE=
Endpoint = 34.84.119.227:51820
AllowedIPs = 10.10.10.0/24, 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16
PersistentKeepalive = 27

# Lets test the connection from the Linux Terminal
sudo cp clientpeer.conf /etc/wireguard/test.conf
sudo chmod 600 /etc/wireguard/test.conf
sudo wg-quick up test
sudo wg show
ping 10.10.10.1
ping 10.0.1.1 (or your LAN gateway)

# You can change Allowed IPS to 0.0.0.0/0, to pass all traffic through the VPN.
sudo vim /etc/wireguard/test.conf
AllowedIPs = 0.0.0.0/0
# Save and exit
sudo wg-quick down test
sudo wg-quick up test
# This should be the OPNsense server IP
curl https://ifconfig.me
```

Firewall Best Practice:
----------------------
Work In progress....


TroubleShooting:
----------------
Caution: Changing the HTTPS web Interface options can break the web interface. 
* If you have broken access to the Web UI by changing settings, please login to the serial console and add this.
```
# Select option 8 
vi /conf/config.xml
# After item , system , group user, Scroll a bit 
<webgui>
# Keep exisitng config
<nohttpreferercheck>1</nohttpreferercheck>
</webgui>
# Save > ESC > :wq!
# Then run the following command:
service configd restart
```

References:
-----------
* https://docs.opnsense.org/
* https://opnsense.org/legal-guidelines/
* https://docs.opnsense.org/manual/how-tos/wireguard-client.html