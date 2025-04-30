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
Login > Dashboard > Firewall > Rules > WAN > Add ( Red Plus Button ) :
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
* Login > Dashboard > Interfaces > Assignment :
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
* Proceed With CAUTION!! This can lock you out of the Webgui and the Serial Console, if done incorrectly. Please test.
* To be safe , you can create a second Admin user to make sure your not locked out of the WebGUI & Can revert changes. 
* Create a Local MFA Server: System > Servers > Add > Description = MFA > Type = Local + Timebased One Time Password > Save 
* Generate USER OTP: System > Access > Users > Edit > OTP Feed > Select Gear ICOn > Save OTP via QR Code or plain Text Code.
* Test MFA Access: System > Tester > Select : Authentication Server = MFA > Enter username > Password = OTP CODE + Password ( EX:123pass )
* Enable MFA Server: System > Settings > Administration > Scroll down to Authetnication > Server = MFA > Save 
* Offical Test: Logout > Login again > username > Password: OTP+Password ( EX: 123pass )
* When MFA is enable, the serial console requires the same password structure > Password: OTP+Password ( EX: 123pass )

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
Password: Decyphertek_01123581321345589
Full Name: System Administrator
Login shell: /bin/csh
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

Wireguard Roadwarrior Setup:
----------------------------
```
* Create the WireGuard server on OPNsense
- VPN > WireGuard > Instances > Add ( Red Plus Button ) :
  - Name: WireguardVPN
  - Generate keys with cogwheel icon
  - Listen Port: 51820
  # Make sure its different than the WAN & LAN Subnet CIDR Ranges.
  - Tunnel Address: 10.10.10.1/24

# Requires a Linux terminal to generate the Wireguard private / public key
# Can use the OPNsense terminal if you dont have access to linux. 
* Create client peer configuration
- VPN > WireGuard > Peers > Add ( Red Plus Button ) :
- Configure with:
  - Enabled: Checked
  - Name: vpnclient
  # To Generate a private / public key for the client
  # OPNsense terminal EX:
  ```
root@OPNsense:~ # wg genkey | tee privatekey | wg pubkey > publickey
root@OPNsense:~ # ls
.cshrc          .login          .mailrc         .shrc           publickey
.history        .login_conf     .profile        .vimrc
.lesshst        .mail_aliases   .rnd            privatekey
root@OPNsense:~ # cat publickey 
  ```
  - Public Key: ( Add output from the cat publickey output ) 
  - Pre-shared Key: ( Click the gear ICON to generate one. )
  - Allowed IPs: 10.10.10.2/32
  - Instances: WiregaurdVPN
  - Keep Alive: 27
  - Save

* Set up interface assignment
- Go to Interfaces → Assignments
- Select the WireGuard device (wg0)
- Add description (WireGuardVPN)
- Enable interface
- Set IPv4/IPv6 Configuration Type to None

* Configure firewall rules
- Create Firewall → Aliases → RFC1918_Networks (192.168.0.0/16 10.0.0.0/8 172.16.0.0/12)
- Add WAN rule to allow client connections to port 51820/UDP
- Add WireGuard interface rule to allow VPN traffic with Destination set to LAN subnet

* Configure split tunneling on client
- Set AllowedIPs on client configuration to only include the LAN subnets
- Example: AllowedIPs = 192.168.1.0/24, 10.0.0.0/8
- This routes only LAN traffic through VPN, internet access uses client's regular connection
```

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