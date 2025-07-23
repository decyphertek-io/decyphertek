Proxmox Virtual Environment is an open-source server virtualization platform that combines KVM hypervisor and LXC container technologies for comprehensive virtualization management. [GCP Marketplace: Proxmox VE]( ) 

Note:
----
* By default Nested Virtualization is disbaled in Google Cloud Platform. 
* Please enable nested virtaulization so KVM / ISO features work properly.
* Modify VM settings via Google Cli on select VMs that support Nested Virtaulization:
```
Supported instance types for nested virtualization:
- N1, N2, N2D, C2, and C2D series VMs
- Recommended: n1-standard-32 or similar with 8+ vCPUs

# GCP CLI
gcloud compute instances list

gcloud compute instances export proxmox-ve \
  --destination=proxmox-config.yaml \
  --zone=us-east1-b

# can use any text editor, doesnt have to be vim. 
vim proxmox-config.yaml
# Add to top
advancedMachineFeatures:
  enableNestedVirtualization: true

gcloud compute instances update-from-file proxmox-ve \
  --source=proxmox-config.yaml \
  --most-disruptive-allowed-action=RESTART \
  --zone=us-east1-b

# Run command from Proxmox terminal to Verify and should return Y .
cat /sys/module/kvm_intel/parameters/nested
```


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