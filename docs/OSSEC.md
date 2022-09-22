OSSEC
=====

An open source host Instrusion detection system.

Install
-------

     $ wget -q -O - https://updates.atomicorp.com/installers/atomic | sudo bash 
     $  sudo apt-get update 
     # Agent Install
     $ sudo apt-get install ossec-hids-agent
     # And/OR - Server Install
     $ sudo apt-get install ossec-hids-server 

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