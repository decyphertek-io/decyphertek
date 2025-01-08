Crowdsec
=====

Crowdsec is an open source Intrusion Prevention System that maintains a global IP blacklist. 

Install:
-------
```
curl -s https://packagecloud.io/install/repositories/crowdsec/crowdsec/script.deb.sh | sudo bash
sudo apt install -y crowdsec crowdsec-firewall-bouncer
sudo apt update
sudo systemctl enable crowdsec
sudo systemctl start crowdsec
sudo systemctl reload crowdsec
sudo systemctl status crowdsec
```

Useful Commands:
---------------
```
sudo cscli collections list
sudo cscli metrics
sudo cscli alerts list
sudo cscli metrics show bouncers
# Interactive config
sudo /usr/share/crowdsec/wizard.sh -c
# Optional:Adjust Firewall Bouncer config 
sudo vim /etc/crowdsec/bouncers/crowdsec-firewall-bouncer.yaml
```

Firewall Bouncer Remediation:
-----------------------------
```
https://docs.crowdsec.net/u/bouncers/blocklist-mirror
sudo apt install crowdsec-blocklist-mirror
```

References
----------
* https://docs.crowdsec.net/docs/getting_started/install_crowdsec/
* https://doc.crowdsec.net/u/bouncers/firewall/


