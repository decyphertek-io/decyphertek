Auditd
=====

Auditd is an open source auditing tool that can increase security and generate reports via auditd logs.    

Install
--------
```
sudo apt install -y auditd audispd-plugins
sudo curl -fsSL -o /etc/audit/rules.d/audit.rules https://raw.githubusercontent.com/decyphertek-io/ansible/refs/heads/main/roles/auditd/files/audit.rules
echo "kernel.audit_backlog_limit=8192" | sudo tee -a /etc/sysctl.conf
sudo tee /etc/audit/auditd.conf > /dev/null <<'CONF'
log_file = /var/log/audit/audit.log
log_format = ENRICHED
log_group = adm
num_logs = 10
max_log_file = 100
max_log_file_action = ROTATE
space_left = 150
space_left_action = SYSLOG
disk_full_action = SYSLOG
CONF
sudo augenrules --load
sudo systemctl enable auditd
sudo systemctl restart auditd
sudo systemctl status auditd
sudo aureport
```

Working with immutbale rules:
----------------------------
```
# Disable the -e2 immutable setting
sudo sed -i 's/^-e 2/#-e 2/' /etc/audit/rules.d/audit.rules
sudo reboot
sudo journalctl -b 0 -t augenrules --no-pager
sudo ausearch -m DAEMON_START,CONFIG_CHANGE -ts boot | grep -i "fail\|error"
# Can edit any failing rules or add new ones. 
sudo vim /etc/audit/rules.d/audit.rules
# Enable the -e2 immutable setting
sudo sed -i 's/^#-e 2/-e 2/' /etc/audit/rules.d/audit.rules
sudo augenrules --load
# Check immutable state was set
sudo augenrules --check
```
  
Watch a directory
-----------------
```
sudo auditctl -w /home/$USER/test_dir/ -k test_watch
```
  
Search Auditd logs
------------------
```
sudo ausearch -k test_watch
```
  
Create a report
----------------
```
sudo ausearch -k test_watch | aureport -f -I 
sudo aureport
```
  
Manage
-------
```
sudo systemctl enable auditd
sudo systemctl start auditd
sudo systemctl restart auditd
sudo systemctl disable auditd
sudo systemctl stop auditd
```

References
----------
* https://www.linux.com/topic/desktop/customized-file-monitoring-auditd/
* https://github.com/Neo23x0/auditd/blob/master/audit.rules
* https://manpages.debian.org/testing/auditd/auditd.8.en.html
* https://linuxhint.com/auditd_linux_tutorial
* https://github.com/Neo23x0/auditd/blob/master/audit.rules
* https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/security_guide/sec-configuring_the_audit_service
* https://bobcares.com/blog/ec2-error-audit-backlog-limit-exceeded/

