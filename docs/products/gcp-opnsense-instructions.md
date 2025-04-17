OPNsense® Firewall/Router/VPN/IDPS is a powerful, open-source network security platform designed for comprehensive protection and management. It provides robust firewall capabilities, secure VPN connections, and advanced intrusion detection and prevention systems to safeguard your network infrastructure. [GCP Marketplace: OPNsense]()

Remote Access:
--------------
* Please enable Serial Console > Launch VM > Click on VM > Edit > enable Remote Access: Enable connecting to serial ports > save
```
# In some cases this feature maybe disable, to enable it from gcloud , run the following command with the right permissions:
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
* Select Option 3: Reset the root password 
```
Enter an option: 3
The root user login behaviour will be restored to its defaults.
Do you want to proceed? [y/N]: Y
Type a new password: 
Confirm new password: 
```
* Select Option 2: Set interface IP address 
```
# The purpose is to regenerate the HTTPS certs, to secure access. 
Enter an option: 2
Configure IPv4 address WAN interface via DHCP? [Y/n] Y
Configure IPv6 address WAN interface via DHCP6? [Y/n] Y
Do you want to change the web GUI protocol from HTTPS to HTTP? [y/N] N
Do you want to generate a new self-signed web GUI certificate? [y/N] Y
Restore web GUI access defaults? [y/N] N
```
* Select option 8: Enter the shell to enable the root account to access the OPNsense Web Dashboard:
```
Enter an option: 8
root@OPNsense:~ # sed -i '' 's/<disabled>1<\/disabled>/<disabled>0<\/disabled>/' /conf/config.xml
root@OPNsense:~ # exit
```
* Select Option 0 : To logout
* You can now visit your IP address and login to the OPNsense Web Dashboard.
```
# Can use Internal or External IP:
# Accept Cert Warning
https://IP-OF-SERVER
Username: root
Password: What you set in option 3.
```

Enable MFA:
-----------
* Create a Local MFA Server: System > Servers > Add > Description = MFA > Type = Local + Timebased One Time Password > Save 
* Generate USER OTP: System > Access > Users > Edit > OTP Feed > Select Gear ICOn > Save OTP via QR Code or plain Text Code.
* Test MFA Access: System > Tester > Select : Authentocation Server = MFA > Enter username > Password = OTP CODE + Password ( EX:123pass )

Optional > Wizard:
----------------
* To customize your settings with help from the Wizard.
* System > Wizard > next > Choose your desired Settings.

Optional > Enable SSH Access:
-----------------------------
* Work In progress......

Optional > Dedicated Admin User, no root:
---------------------------------------
Work in progress....

References:
-----------
https://docs.opnsense.org/