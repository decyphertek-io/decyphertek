Auditd
=====

Auditd is an open source auditing tool that can increase security and generate reports via auditd logs.    

Install
--------

     $ sudo apt install -y auditd audispd-plugins
     $ sudo su -c "curl 'https://raw.githubusercontent.com/decyphertek-io/ansible/main/roles/auditd/files/audit.rules' >> /etc/audit/rules.d/audit.rules"
     $ sudo su -c "curl 'https://raw.githubusercontent.com/decyphertek-io/ansible/main/roles/auditd/files/audit.rules' >> /etc/audit/audit.rules"
     $ sudo systemctl enable auditd
     $ sudo systemctl restart auditd
     $ sudo systemctl status auditd
  
Watch a directory
-----------------

     $ sudo auditctl -w /home/[your_user_name]/test_dir/ -k test_watch
  
Search Auditd logs
------------------

     $ sudo ausearch -k test_watch
  
Create a report
----------------

     $ sudo ausearch -k test_watch | aureport -f -I 
     $ sudo aureport
  
Manage
-------

     $ sudo systemctl enable auditd
     $ sudo systemctl start auditd
     $ sudo systemctl restart auditd


References
----------

     https://www.linux.com/topic/desktop/customized-file-monitoring-auditd/
     https://github.com/Neo23x0/auditd/blob/master/audit.rules
     https://manpages.debian.org/testing/auditd/auditd.8.en.html
     https://linuxhint.com/auditd_linux_tutorial
     https://github.com/Neo23x0/auditd/blob/master/audit.rules
     https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/security_guide/sec-configuring_the_audit_service
     https://bobcares.com/blog/ec2-error-audit-backlog-limit-exceeded/
 
