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

