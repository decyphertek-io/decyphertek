Proxmox Virtual Environment is an open-source server virtualization platform that combines KVM hypervisor and LXC container technologies for comprehensive virtualization management. [GCP Marketplace: Proxmox VE]( ) 

SSH Access:
-----------
* Utilize OS-Login OR add ssh keys via security & Access > SSH Keys > ssh-rsa KEY adminotaur
```
ssh adminotaur@ip-of-server
# OR: If using OS Login
sudo su adminotaur
cd ~
```

Login to Proxmox VE:
--------------------
* Please ssh into the Proxmox VE Virtual machine and create a password.
```
# Proxmox VE uses local PAM Authentication.
sudo passwd adminotaur
```
* login to Proxmox Dashboard:
```
https://IP-OF-SERVER
Username: adminotaur
Password: # SET PASSWORD AS MENTIONED
```
* The pop up suggests a Proxmox support Subscription, this is optional.
* If you would like Proxmox enterprise support:
```
https://www.proxmox.com/en/products/proxmox-virtual-environment/pricing
```

Security Features:
------------------
* OSSEC HIDS - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/
* Rsyslog - https://www.rsyslog.com/doc/index.html
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and daily.
* Security Report - Daily security report found at /var/log/decyphertek/

References:
-----------
* https://pve.proxmox.com/pve-docs/