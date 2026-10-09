
Decyphertek has secured your Azure VM with one or more of the following open source software. Please reference the specific softare stack your server has. As a courteousy to Azure Subscribers this section can be used as a quick reference. [Azure Marketplace: Decyphertek ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=decyphertek.io&page=1)

Security Features
-----------------

* Note: After 4/19/26 , Removed Crowdsec, Quad9 DNS, Modsecurity & Unattended Upgrades.
  Added Ossec , Rsyslog & Automated Updates.
* OSSEC HIDS - An open source Host Intrusion Detection System that monitors logs & file integrity.
* UFW Host Firewall - A host based firewall that adds an addtional layer of security to limit access to your server.
* Automated Updates - Update script upon first boot and daily.
* Auditd Logging - Provides additional security logging based of security aduitd rules set.
* Rsyslog - System logging service for centralized logging.


OSSEC HIDS:
----------
* A Host Intrusion Detection System. Monitors logs, rootkit detection & file integrity.
* Check status ( ssh into the server, run with sudo ):
```
sudo /var/ossec/bin/ossec-control status
sudo systemctl status ossec
```
* View recent alerts:
```
sudo tail -20 /var/ossec/logs/alerts/alerts.log
sudo tail -f /var/ossec/logs/alerts/alerts.log
```
* Restart the service after config changes ( /var/ossec/etc/ossec.conf ):
```
sudo /var/ossec/bin/ossec-control restart
```

UFW Host Firewall:
-----------------
* Check status & rules:
```
sudo ufw status
sudo ufw status verbose
sudo ufw status numbered
```
* Allow / deny a port:
```
sudo ufw allow 443/tcp
sudo ufw deny 23/tcp
```
* Remove a rule ( by number or by spec ):
```
sudo ufw status numbered
sudo ufw delete 2
sudo ufw delete allow 443/tcp
```
* View firewall logs:
```
sudo tail -20 /var/log/ufw.log
```
* Note: Azure network security group rules also apply, check those in the Azure console.

Auditd Logging:
--------------
* Check the service:
```
sudo systemctl status auditd
```
* Summary report of today's activity:
```
sudo aureport -ts today
```
* Search today's security events:
```
sudo ausearch -m AVC,USER_AVC,SELINUX_ERR -ts boot -i
sudo ausearch --start today --interpret
```
* List the active rules & where they live:
```
sudo auditctl -l
sudo cat /etc/audit/rules.d/*.rules
```

Automated Updates:
-----------------
* Your server updates itself: an update script runs on first boot and once daily via crontab.
* Run the updates manually ( anytime ):
```
sudo bash /opt/.update.sh
```
* View the schedule:
```
sudo crontab -l
```
* Check when it last ran:
```
sudo grep -i update /var/log/cron*
```

Rsyslog:
--------
* Central system logging. Check & restart:
```
sudo systemctl status rsyslog
sudo systemctl restart rsyslog
```
* Watch the logs live:
```
sudo tail -f /var/log/syslog
```
* Review recent errors & warnings:
```
sudo grep -Ei "error|fail|warning|critical" /var/log/syslog | tail -20
```
* Daily Security Report - combines Auditd + OSSEC + Rsyslog into one daily summary ( scheduled via crontab ):
```
cd /var/log/decyphertek/
ls
sudo cat security_report_DATE-HERE.log
```

References:
-------------

    https://www.ossec.net/docs/
    https://wiki.ubuntu.com/UncomplicatedFirewall
    https://github.com/linux-audit
    https://www.rsyslog.com/doc/
    https://man7.org/linux/man-pages/man8/cron.8.html
