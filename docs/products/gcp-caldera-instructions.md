Mitre Caldera V5 is an advanced, open-source platform designed for adversary emulation and automated red teaming. It allows users to simulate various cyber attack techniques and tactics in a controlled environment, providing valuable insights for improving cybersecurity defenses.

Note:
-----
* Please be patient , it takes 5-10 minutes for Mitre Caldera to be accessible. 

SSH:
--------------------
* Utilize Google SSH Console or setup ssh keys or password.

Passwords:
----------
* To Get all the Mitre Caldera Passwords , run the follwoing command from terminal:
```
sudo cat /home/adminotaur/caldera/conf/local.yml
```

Login:
------
* login to your Mitre Caldera V5:
````
https://IP-OF-YOUR-VM:8443
````
* Note: It is set to use a public IP , please see troublehsooting to customize to a private IP.
* How to login as the Red or blue user:
````
username: red
password: ( sudo cat /home/adminotaur/caldera/conf/local.yml | grep red )

username: blue
password: ( sudo cat /home/adminotaur/caldera/conf/local.yml | grep blue )
````
Plugin Ports:
-------------
* Note: UFW Host firewall is only set to allow port 22 & 8443 by default.
```
# To allow access to any of the ports mentioned , add a rule.
EX:
sudo ufw allow 8853/tcp
sudo ufw allow 8853/udp

# Check the current firewall rules:
sudo ufw status numbered

# Delete a rule, select a numbered from the above command:
sudo ufw delete 99
```
* DNS Contact Plugin (Port 8853)
- Description: Handles agent communication via DNS.
- Test: Configure an agent to use DNS and verify it registers successfully.
- Expected Outcome: Agent should appear in the Caldera interface.

* FTP Contact Plugin (Port 2222)
- Description: Handles agent communication via FTP.
- Test: Use an FTP client to connect, upload, and download files.
- Expected Outcome: Successful file transfers.

* TCP Contact Plugin (Port 7010)
- Description: Handles agent communication via TCP.
- Test: Deploy an agent over TCP and monitor the connection.
- Expected Outcome: Stable TCP connection and communication.

* UDP Contact Plugin (Port 7011)
- Description: Handles agent communication via UDP.
- Test: Deploy an agent over UDP and verify packet exchange.
- Expected Outcome: Successful data transmission with minimal packet loss.

* WebSocket Contact Plugin (Port 7012)
- Description: Handles agent communication via WebSocket.
- Test: Deploy an agent over WebSocket and confirm the connection.
- Expected Outcome: Real-time communication via WebSocket.

* SSH Tunnel Plugin (Port 8022)
- Description: Enables agent communication through SSH tunnels.
- Test: Establish an SSH tunnel and deploy an agent.
- Expected Outcome: Secure communication through the tunnel.

* HTTP/HTTPS Contact Plugin (Port 8443)
- Description: Facilitates agent communication via HTTP/HTTPS.
- Test: Access the web interface and deploy an agent.
- Expected Outcome: Secure agent registration via HTTPS.

* Main Web Interface (Port 8888)
- Description: Central interface for Caldera operations.
- Test: Log in and perform basic operations.
- Expected Outcome: Full functionality with no errors.

Troubleshooting:
----------------
* If you need update the IP or other data in local.yml
```
sudo systemctl stop caldera
sudo vim /home/adminotaur/caldera/conf/local.yml
# If you want to use a private Ip , instead of public, change the following:
app.contact.http: https://IP-OF-YOUR-SERVER:8443
app.frontend.api_base_url: https://IP-OF-YOUR-SERVER:8443

# make sure to also change the IP here as well:
sudo vim /home/adminotaur/caldera/plugins/magma/.env
VITE_CALDERA_URL=https://IP-OF-YOUR-SERVER:8443

# Once these are updated, run the follwing command:
sudo systemctl start caldera-build
# Wait a couple of minutes for it to build, once you see Caldera in status, build is done.
sudo systemctl status caldera-build
# Once Caldera is visible, you can stop the service.
sudo systemctl stop caldera-build
# Now you can start Caldera.
sudo systemctl start caldera

```
* To get the plugins to work, you need to allow them via UFW host firewall:
```
# Check the plugin ports section, EX:
sudo ufw allow 8853/tcp
sudo ufw allow 8853/udp

# Check the current firewall rules:
sudo ufw status numbered

# Delete a rule, select a numbered from the above command:
sudo ufw delete 99
```
Security Features:
-------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and daily.

References:
-----------
* https://caldera.readthedocs.io/en/latest/