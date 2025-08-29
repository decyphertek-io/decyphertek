Proxmox Virtual Environment is an open-source server virtualization platform that combines KVM hypervisor and LXC container technologies for comprehensive virtualization management. [Azure Marketplace: Proxmox VE ]( )


Note:
----
* Proxmox VE requires Virtual Machines that support nested Virtualization:
```
# Azure VM Sizes with Nested Virtualization Support & Pricing (East US region)
Standard_F4_v2 $0.168/hour - 4 vCPUs, 8 GB RAM
Standard_D4_v3 $0.192/hour - 4 vCPUs, 16 GB RAM
Standard_E4_v3 $0.252/hour - 4 vCPUs, 32 GB RAM
Standard_F8_v2 $0.336/hour - 8 vCPUs, 16 GB RAM
Standard_D8_v3 $0.384/hour - 8 vCPUs, 32 GB RAM
Standard_E8_v3 $0.504/hour - 8 vCPUs, 64 GB RAM
```

SSH Access:
-----------
* Utilize Azure to setup user and ssh keys. 
* Make sure to allow ssh, https via network security group.

Login to Proxmox VE:
--------------------
* Please ssh into the Proxmox VE Virtual machine and create a password.
```
# Proxmox VE uses local PAM Authentication.
sudo passwd root
OR
sudo passwd USERNAME
```
* login to Proxmox Dashboard:
```
https://IP-OF-SERVER
Username: root or USERANEM
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
* Now, when you create a VM or container, can select your iso or container template.
```
# EX: Add to ISO URL in GUI. ( Best to get the newest link and checksum directly from a trusted website )
Kali Linux: https://cdimage.kali.org/kali-2025.2/kali-linux-2025.2-installer-amd64.iso
Name: kali.iso
sha256: 5723d46414b45575aa8e199740bbfde49e5b2501715ea999f0573e94d61e39d3

# CT Templates : 
# List available templates
sudo pveam available

# Download a template (example) ( From Terminal: SSH In )
sudo pveam download local debian-12-standard_12.7-1_amd64.tar.zst
sudo pveam download local rockylinux-9-default_20240912_amd64.tar.xz
sudo pveam download local almalinux-9-default_20240911_amd64.tar.xz
sudo pveam download local ubuntu-25.04-standard_25.04-1.1_amd64.tar.zst
sudo pveam download local archlinux-base_20240911-1_amd64.tar.zst
sudo pveam download local fedora-42-default_20250428_amd64.tar.xz

# Create a Container
Proxmox UI > Create CT > Template: Select the template you downloaded.

# Please be Patient
Sometimes the console window for the container can take up to 5 mins to load properly.
You may have to also press enter to get the login to show.

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
* NGINX - https://nginx.org/en/docs/
* Automated Updates - Update script upon first boot and daily.
* Security Report - Daily security report found at /var/log/decyphertek/

References:
-----------
* https://pve.proxmox.com/pve-docs/