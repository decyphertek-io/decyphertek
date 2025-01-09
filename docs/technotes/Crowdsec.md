Crowdsec
=====

Crowdsec is an open source Intrusion Prevention System , with an optional firewall bouncer. 

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
sudo apt install -y rsyslog
sudo cp /etc/rsyslog.conf /etc/rsyslog.conf.bak
# Rsyslog config ( Crowdsec supports: RFC3164 or RFC5424 & up to 2048 bytes )
sudo vim /etc/rsyslog.conf

$ModLoad imuxsock
$ModLoad imklog

$FileOwner root
$FileGroup root
$FileCreateMode 0640
$DirCreateMode 0755
$Umask 0022
$WorkDirectory /var/spool/rsyslog
$IncludeConfig /etc/rsyslog.d/*.conf

$MaxMessageSize 2048

auth,authpriv.*                 /var/log/auth.log
*.*;auth,authpriv.none          -/var/log/syslog
#cron.*                         /var/log/cron.log
daemon.*                        -/var/log/daemon.log
kern.*                          -/var/log/kern.log
lpr.*                           -/var/log/lpr.log
mail.*                          -/var/log/mail.log
user.*                          -/var/log/user.log

mail.info                       -/var/log/mail.info
mail.warn                       -/var/log/mail.warn
mail.err                        /var/log/mail.err

news.crit                       /var/log/news/news.crit
news.err                        /var/log/news/news.err
news.notice                     -/var/log/news/news.notice

*.=debug;\
        auth,authpriv.none;\
        news.none;mail.none     -/var/log/debug
*.=info;*.=notice;*.=warn;\
        auth,authpriv.none;\
        cron,daemon.none;\
        mail,news.none          -/var/log/messages

*.emerg                         :omusrmsg:*

daemon.*;mail.*;\
        news.err;\
        *.=debug;*.=info;\
        *.=notice;*.=warn       |/dev/console


sudo systemctl daemon-reload
sudo systemctl enable rsyslog
sudo systemctl start rsyslog
sudo cscli collections install crowdsecurity/linux
sudo cscli collections install crowdsecurity/sshd
sudo cscli collections install crowdsecurity/auditd
# Check your log paths
sudo ls /var/log/
# Make sure to make a yaml under crowdsec to collect the logs:
sudo vim /etc/crowdsec/acquis.yaml
# I added adutid log & Removed the unused ones.

# Authentication and syslog-ng logs
filenames:
  - /var/log/auth.log
  - /var/log/syslog
labels:
  type: syslog

---

# Auditd logs
filenames:
  - /var/log/audit/audit.log
labels:
  type: auditd

sudo systemctl reload crowdsec
sudo cscli collections list
# Use the same logic for the rest. 
# Testing Crowdsec Log ingestion:
logger "This is a test log entry for rsyslog."
echo "Test log entry for audit.log" | sudo tee -a /var/log/audit/audit.log
sudo cscli metrics show acquisition
# Troubelshooting syslog parser issues:
sudo su -c "tail -n 10 /var/log/syslog | cscli explain -f- --type syslog"
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


