OSSEC
=====

An open source host Instrusion detection system.

Simple Install
-------

     $ wget -q -O - https://updates.atomicorp.com/installers/atomic | sudo bash 
     $ sudo mv /etc/apt/trusted.gpg /etc/apt/trusted.gpg.d/ossec.gpg
     $ sudo apt-get update 
     # Agent Install
     $ sudo apt-get install ossec-hids-agent
     # And/OR - Server Install
     $ sudo apt-get install ossec-hids-server 

Install from Github
-------------------

     # Install dependencies : ( View any errors and install additonal dependices if needed. )
     $ sudo apt install git libpcre2-dev openssl libssl-dev libsystemd-dev zlib1g-dev
     $ git clone https://github.com/ossec/ossec-hids.git
     $ cd ossec-hids
     $ sudo su -c "./install.sh"
     # choose: local, agent, server, or hybrid. See help for descriptions. 
     $ sudo /var/ossec/bin/ossec-control start
     $ sudo /var/ossec/bin/ossec-control status
     # Create an ossec service , so it starts at reboot.
     $ sudo vim /etc/systemd/system/ossec.service

     [Unit]
     Description=OSSEC Host-Based Intrusion Detection System
     After=network.target

     [Service]
     Type=forking
     ExecStart=/var/ossec/bin/ossec-control start
     ExecStop=/var/ossec/bin/ossec-control stop
     Restart=always
     User=root

     [Install]
     WantedBy=multi-user.target

     $ sudo systemctl daemon-reload
     $ sudo systemctl enable ossec.service
     $ sudo systemctl start ossec.service
     $ sudo systemctl status ossec.service

Example 1: Show Successful Logins
---------------------------------

     $ sudo su 
     # Or run cron as root
     # cat /var/ossec/logs/alerts/alerts.log | /var/ossec/bin/ossec-reportd -f group authentication_success 

Example 2: Show Alerts Level 10 and Greater
-------------------------------------------

     # cat /var/ossec/logs/alerts/alerts.log | /var/ossec/bin/ossec-reportd -f level 10 

Example 3: Show the src-ip for all users
---------------------------------------

     # cat /var/ossec/logs/alerts/alerts.log | var/ossec/bin/ossec-reportd -f group authentication -r user srcip

Example 4: Show Changed files as reported by Syscheck
------------------------------------------------------

     # cat /var/ossec/logs/alerts/alerts.log | /var/ossec/bin/ossec-reportd -f group
     # cat /var/ossec/logs/alerts/alerts.log | /var/ossec/bin/ossec-reportd 2>&1 | more

Optional: Local install Desktop Notifications:
-----------------------------------------------

     # Limitations, only alerts you when you have an active desktop session. 
     # Dependencies Required
     $ sudo apt install libnotify-bin
     $ sudo vim /etc/systemd/system/ossec-alerts.service
     #Replace $user with your desktop user. 

     [Unit]
     Description=OSSEC Alert Check Service
     After=network.target

     [Service]
     Type=simple
     User=$USER
     Environment="DISPLAY=:0"
     # Please run this command to find right data - printenv DBUS_SESSION_BUS_ADDRESS
     Environment="DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus"
     ExecStart=/bin/bash -c 'while true; do logs=$(timeout 60 /usr/bin/tail -n0 -F /var/ossec/logs/alerts/alerts.log); if [ -n "$logs" ]; then /usr/bin/notify-send "OSSEC Alerts" "$logs"; fi; sleep 1; done'

     [Install]
     WantedBy=multi-user.target

     # Replace $user with your desktop user. 
     $ sudo chown -R $USER:ossec /var/ossec/logs/alerts/alerts.log
     $ sudo chown -R $USER:root /usr/bin/tail

     # Enable the service
     $ sudo systemctl daemon-reload
     $ sudo systemctl enable ossec-alerts.service
     $ sudo systemctl start ossec-alerts.service

     # Test the ossec alert notification - wait up to one minute. ( Integrity Check must be enabled . )
     $ sudo apt install htop -y && sudo apt purge htop -y && sudo apt install htop -y


References
----------

     https://www.ossec.net/download-ossec/