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
     $ sudo apt install git libpcre2-dev openssl libssl-dev libsystemd-dev
     $ git clone https://github.com/ossec/ossec-hids.git
     $ cd ossec-hids
     $ sudo su -c "./install.sh"
     # choose: local, agent, server, or hybrid. See help for descriptions. 
     $ sudo /var/ossec/bin/ossec-control start
     $ sudo /var/ossec/bin/ossec-control status

Example 1: Show Successful Logins
---------------------------------

     $ sudo su 
     # Or run cron as root
     # cat /var/ossec/logs/alerts/alerts.log | /var/ossec/bin/ossec-reportd -f group authentication_success 

Example 2: Show Alerts Level 10 and Greater
-------------------------------------------

     # cat /var/ossec/logs/alerts/alerts.log | /var/ossec/bin/ossec-reportd -f level 10 

Example 3: Show the srcip for all users
---------------------------------------

     # cat /var/ossec/logs/alerts/alerts.log | var/ossec/bin/ossec-reportd -f group authentication -r user srcip

Example 4: Show Changed files as reported by Syscheck
------------------------------------------------------

     # cat /var/ossec/logs/alerts/alerts.log | /var/ossec/bin/ossec-reportd -f group
     # cat /var/ossec/logs/alerts/alerts.log | /var/ossec/bin/ossec-reportd 2>&1 | more


References
----------

     https://www.ossec.net/download-ossec/