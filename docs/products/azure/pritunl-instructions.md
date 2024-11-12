Pritunl is an Enterprise VPN Server that supports OpenVPN & WireGuard. .It is designed for simplicity, reliability, and flexibility, making it suitable for both small businesses and large enterprises. [Azure Marketplace: Pritunl VPN Server ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/decyphertek.pritunl_vpn?tab=Overview)

Note:
------
* Please be aware that it takes a few minutes for Pritunl VPN Server to be up and running.

SSH Into the server:
--------------------
* Utilize Azure SSH settings to set your ssh keys AND/OR Password to ssh in. 

Pritunl Login:
----------------
* ssh into your server
```
sudo pritunl setup-key
```
* Add the key to the new VPN server ( Takes a few minutes to be accessible )
* Make sure your network security group in Azure that is assigned to your VM allows inbound 443/tcp , 1194/udp , and 51820/udp.
```
https://ip-of-server
```
* Once you enter the key , you will get disconnected, the database is being setup.
* To get the auto-generated login password , type from terminal
```
sudo pritunl default-password
```
* Once you login , you will immediately be sent to a page to change the password .
* Secure Pritunl & Allow Wireguard to work properly ( Requires setup-key to be done first, as mentioned before ):
```
sudo pritunl set app.reverse_proxy true
sudo pritunl set app.redirect_server false
sudo pritunl set app.server_ssl true
sudo pritunl set app.server_port 443
sudo systemctl restart pritunl
```

Pritunl VPN Setup:
-----------------
* To get connected to a vpn server on Pritunl an organization, user and server must be created.
* Login > Users > select Add Organization > Save > Add User > requires creating a PIN
* You can decide to use two factor or not, click the Qrcode and use google authetnicator.
* Now you need to create a server
* Login > Servers > Select Add Server
* This will autopopulate the basic settings , you can change them how you like.
```
OpenVPN Default Port/Protocol: 1194/udp
```
* Click enable wireguard if you want to use it and add the following port number
```
Wireguard Default Port/Protocol: 51820/udp
```
* You can also enable google authenticator for MFA.
* Add a Wg virtual network , can not be the same as the default openvpn one above.
* EX: 192.168.235.0/24
* Save it and attach an organization
* Now start the server
* Download the Pritunl VPN Client: 
```
https://client.pritunl.com/
```
* Download and import the VPN profile for the user:
* login > user > select the download icon > Optional: Select the QR code icon to setup MFA.
* OR
* login > user > select URI > Link is valid for 24 hrs.
* Once downloaded, you can import to the client. Select OpenVPN or Wiregaurd to connect.
* Note: Wireguard needs to also be installed on the client to use Wireguard.
```
https://www.wireguard.com/install/
```
* Optional: Client side Conflicts - On linux based systems (Debian) , to get Wireguard to work, need to install resolvconf. This will break OpenVPN.
```
sudo apt install resolvconf
```

NOTE: Configuring Server Routes:
-------------------------------
Server routes control what traffic will be tunneled over the vpn server. By default a server will include the 0.0.0.0/0 route. This route will tunnel all internet traffic over the vpn server. To only route a local network on the vpn server first remove the 0.0.0.0/0 route and click Add Route to add the local network route such as 192.168.0.0/24.

Security Features:
------------------
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Updates happen daily via crontab. 

Troubleshooting:
----------------
* UFW Firewall is only set to allow ports , 443 , 22 , 1194 , and 51820. 
* If you use a different port , please add a firewall rule. EX: sudo ufw allow port/protocol
```
sudo ufw allow 51820/udp
```
* If you want to remove access to a port and delete the firewall rule. EX: sudo ufw delete number
```
sudo ufw status numbered
sudo ufw delete 99
```
References:
-----------
* https://client.pritunl.com/
* https://www.wireguard.com/install/
* https://docs.pritunl.com/docs/wireguard
* https://docs.pritunl.com/docs/getting-started
