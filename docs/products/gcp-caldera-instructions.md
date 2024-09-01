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

Security Features:
-------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and daily.

References:
-----------
* https://caldera.readthedocs.io/en/latest/