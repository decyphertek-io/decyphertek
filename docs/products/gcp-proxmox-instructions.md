Proxmox Virtual Environment is an open-source server virtualization platform that combines KVM hypervisor and LXC container technologies for comprehensive virtualization management. [GCP Marketplace: Proxmox VE]( ) 

Note:
----
* By default Nested Virtualization is disabled in Google Cloud Platform. 
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

Creating VMs:
------------
* Optional: A few difffernt examples.
* Upload an ISO > Datacenter > Proxmox-ve > local > ISO Images> Upload or Download from URL.
```
# EX: Add to ISO URL in GUI. ( Best to get the newest link and checksum directly from a trusted website )
Xubuntu 24: https://mirror.us.leaseweb.net/ubuntu-cdimage/xubuntu/releases/24.04/release/xubuntu-24.04.2-desktop-amd64.iso
Name: xubuntu.iso
sha256: ba76abf526b4c7ab22e8125cca69547f76559f703bd357c54bdf5d74be0bfd2b

# CT Templates : 
# List available templates
sudo pveam available

# Download a template (example)
sudo pveam download local debian-12-standard_12.7-1_amd64.tar.zst
sudo pveam download local rockylinux-9-default_20240912_amd64.tar.xz
sudo pveam download local almalinux-9-default_20240911_amd64.tar.xz
sudo pveam download local ubuntu-25.04-standard_25.04-1.1_amd64.tar.zst
sudo pveam download local archlinux-base_20240911-1_amd64.tar.zst
sudo pveam download local fedora-42-default_20250428_amd64.tar.xz

# Troubleshooting
sudo cat /var/log/ufw.log | grep BLOCK
sudo pct list
sudo pct status 100
dpkg -l | grep pve-container

# ParrotOS EX: How to convert OVA to Qcow or just to use Qcow images. 
wget https://deb.parrot.sh/parrot/iso/6.4/Parrot-home-6.4_amd64.ova
tar -xvf Parrot-home-6.4_amd64.ova
qemu-img convert -f vmdk -O qcow2 Parrot-home-mate-6.4_amd64-disk001.vmdk parrots-6.4-home-mate.qcow2
sudo mkdir -p /var/lib/vz/template/qcow
sudo mv parrots-6.4-home-mate.qcow2 /var/lib/vz/template/qcow/
# Create a VM first:
# OS: no media format 
# Disk: Bus/Device - VirtIO
# Import qcow to the vm 
cd /var/lib/vz/template/qcow/
sudo qm importdisk 100 parrots-6.4-home-mate.qcow2 local
# Attach qcow to vm after importing. 
# Select VM >  hardware > select unused disk > edit > add 
# This is a good example of how to convert ova to qcow2 & import qcow2 to proxmox
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