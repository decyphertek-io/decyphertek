UFW
=====

Uncomplicated Firewall {UFW} is a host based firewall availble on debian based systems. A simple way to
manage access to ports & protocols. 

Install
-------

    sudo apt install ufw
    sudo ufw limit 22/tcp
    sudo ufw allow https
    sudo ufw enable
    sudo ufw status verbose
  
Delete rules
------------

    sudo ufw status numbered
    sudo ufw delete number
    # Delete all rules
    sudo ufw reset

Examples
--------

    # Allow outbound via port/protocol
    sudo ufw allow out 853
    sudo ufw allow out 853/tcp
    # Allow inbound via port/protocol
    sudo ufw allow in 443
    sudo ufw allow in 443/tcp
    # Allow via port/protocol
    sudo ufw allow 22
    sudo ufw allow 22/tcp
    # Allow via service/protocol
    sudo ufw allow ssh
    sudo ufw allow ssh/tcp
    # Deny via port/protocol
    sudo ufw deny 22
    sudo ufw deny 22/tcp
    # Deny via service/protocol
    sudo ufw deny ssh
    sudo ufw deny ssh/tcp
    # Limit connection, blocks after six attemps for 30 secs. 
    sudo ufw limit 22/tcp
    sudo ufw limit 3389/tcp

Troubleshooting
----------------

    sudo apt install rsyslog
    sudo systemctl enable rsyslog
    sudo systemctl start rsyslog
    sudo systemctl status rsyslog
    # on, low, medium , high, or full 
    sudo ufw logging on
    sudo ufw logging low
    sudo ls /var/log/ufw*
    # Read all the logs
    sudo less /var/log/ufw* 
    # Search an issue. 
    sudo less /var/log/ufw* | grep 'BLOCK'


References
----------

    https://linuxhint.com/ufw_list_rules/
    https://manpages.ubuntu.com/manpages/bionic/man8/ufw.8.html
    https://www.linux.com/training-tutorials/introduction-uncomplicated-firewall-ufw/
