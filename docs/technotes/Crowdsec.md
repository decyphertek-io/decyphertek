Crowdsec
=====

Crowdsec is an open source Intrusion Prevention System that maintains a global IP blacklist. 

Install
-------

     $ curl -s https://packagecloud.io/install/repositories/crowdsec/crowdsec/script.deb.sh | sudo bash
     $ sudo apt install -y crowdsec crowdsec-firewall-bouncer-iptables
     $ sudo systemctl enable crowdsec
     $ sudo systemctl start crowdsec
     $ sudo systemctl reload crowdsec
     $ sudo systemctl status crowdsec

Useful Commands
---------------

     $ sudo cscli collections list
     $ sudo cscli metrics
     $ sudo cscli alerts list
     # Interactive config
     $ sudo /usr/share/crowdsec/wizard.sh -c
  
References
----------

     https://docs.crowdsec.net/docs/getting_started/install_crowdsec/


