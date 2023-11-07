Pritunl is an open source VPN server that supports Wireguard & Openvpn. 

Pritunl Login:
----------------
* ssh into your server
* ssh adminotaur@ip-of-server
* sudo pritunl setup-key
* Add the key to the new VPN server ( Takes a few minutes to be accessible )
* https://ip-of-server
* Once you enter the key , you will get disconnected, the database is being setup
* Please be patient and try after a few minutes.
* To get the auto-generated login password , type from terminal
* sudo pritunl default-password
* Once you login , you will immediately be sent to a page to change the password .

Pritunl VPN Setup:
-----------------
* To get connected to a vpn server on Pritunl an organization, user and server must be created.
* Login > Users > select Add Organization > Save > Add User > requires creating a PIN
* You can decide to use two factor or not, click the Qrcode and use google authetnicator.
* Now you need to create a server
* Login > Server > Select Add Server
* This will autopopulate the basic settings , you can change them how you like.
* If you do , remember to add the ufw rule and the security group rule.
* The default port is 1194 ( OpenVPN )
* Click enable wireguard if you want to use it and add the following port number
* wg port number - 51820
* You can also enable google authenticator for MFA.
* Add a Wg virtual network , can not be the same as the default openvpn one above.
* EX: 192.168.228.0/24
* Save it and attach an organization
* Now start the server
* Its important to allow this traffic on the security groups and UFW Firewall.
* sudo ufw allow 51820/udp
* OR / AND
* sudo ufw allow 1194/udp
* To use wireguard, the VPN client user must also have access to port 443, make sure to allow them in the AWS Security group.
* Note: This is not the case if you just use OpenVPN, just required for Wireguard.
* Download the Pritunl VPN Client - https://client.pritunl.com/
* Download and import the VPN profile for the user
* login > user > select the download icon > Optional: Select the QR code icon to setup MFA.
* OR
* login > user > select URI > Link is valid for 24 hrs.
* Once downloaded, you can import to the client. Select OpenVPN or Wiregaurd to connect.
* Note: Wiregaurd needs to also be installed on the client to use Wireguard.
* https://www.wireguard.com/install/

Refernces:
-----------
https://www.wireguard.com/install/
https://client.pritunl.com/
https://docs.pritunl.com/docs/getting-started

