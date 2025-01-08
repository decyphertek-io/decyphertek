Crowdsec
=====

Crowdsec is an open source Intrusion Prevention System that maintains a global IP blacklist. 

Install:
-------
```
curl -s https://packagecloud.io/install/repositories/crowdsec/crowdsec/script.deb.sh | sudo bash
sudo apt install -y crowdsec 
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
sudo cscli bouncers list
sudo cscli decisions list
sudo cscli metrics show bouncers
# Interactive config
sudo /usr/share/crowdsec/wizard.sh -c
```

Install Collections:
-------------------
```
sudo cscli collections install crowdsecurity/linux
sudo cscli collections install crowdsecurity/auditd
sudo cscli collections install crowdsecurity/iptables
sudo cscli collections install crowdsecurity/sshd
sudo cscli collections install crowdsecurity/nginx
sudo systemctl reload crowdsec
```

Firewall Bouncer Remediation:
-----------------------------
```
#ipset lists have to exist before crowdsec-firewall-bouncer starts. You can create them and add them to your iptables like this:
sudo ipset flush
sudo ipset create crowdsec-blacklists hash:ip timeout 0 maxelem 150000
sudo ipset create crowdsec6-blacklists hash:ip timeout 0 family inet6 maxelem 150000
sudo iptables -I INPUT 1 -m set --match-set crowdsec-blacklists src -j DROP
sudo ip6tables -I INPUT 1 -m set --match-set crowdsec6-blacklists src -j DROP
sudo su -c "ipset save > /etc/ipset.conf"
sudo vim /usr/lib/systemd/system/ipset.service
# Replace Execstart with the following:
ExecStart=/usr/bin/ipset -exist -f /etc/ipset.conf restore
# Hit esc and save
esc > :wq!
sudo systemctl enable ipset.service
sudo systemctl start ipset.service
sudo ipset list
sudo apt install -y crowdsec-firewall-bouncer-iptables crowdsec-blocklist-mirror
sudo systemctl enable crowdsec-firewall-bouncer-iptables crowdsec-blocklist-mirror
sudo systemctl start crowdsec-firewall-bouncer-iptables crowdsec-blocklist-mirror
sudo cscli bouncers list
# Optional:Adjust Firewall Bouncer config 
sudo vim /etc/crowdsec/bouncers/crowdsec-firewall-bouncer.yaml
```

Register Crowdsec API:
---------------------
```
sudo cscli capi register
sudo cscli capi status
```

References
----------
* https://docs.crowdsec.net/docs/getting_started/install_crowdsec/
* https://doc.crowdsec.net/u/bouncers/firewall/
* https://docs.crowdsec.net/u/bouncers/blocklist-mirror


