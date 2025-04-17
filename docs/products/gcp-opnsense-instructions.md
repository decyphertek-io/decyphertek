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
* Select Option 3: Set the root password 
* Select Option 2: Setup IP , to regenerate new SSl certs
* Select option 8: Enter the shell and run the following command:
```
# This will enable the root acocunt for the WebGUI Login
sed -i '' 's/<disabled>1<\/disabled>/<disabled>0<\/disabled>/' /conf/config.xml
```
* You can now visit your IP address and login to the OPNsense Web Dashboard.
```
https://IP-OF-SERVER
Username: root
Password: What you set in option 3.
```

Optional: Dedicated Admin User, no root:
---------------------------------------
Work in progress....

References:
-----------
