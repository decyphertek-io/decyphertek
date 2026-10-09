Azure Basics
----------

If you're new to Azure and need a quick reference guide, this is a good place to start. [Azure Marketplace: Decyphertek ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=decyphertek.io&page=1)

SSH Keys:
--------
* Create or use a key pair for secure SSH access to your Azure VMs.
* Docs: https://learn.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys
* Azure Portal > Create a VM > SSH public key > Use existing key pair, or select Generate new key pair and download the private key.
* You can also create a key pair Linux / macOS / Cloud Shell:
```
ssh-keygen -t rsa -b 4096
ssh-keygen -t ed25519
```
* Supported key types: RSA ( 2048-bit minimum ) or ED25519. Save the private key as .pem if you plan to use it with ssh on Linux / macOS.
* Permissions: If you use a .pem key on Linux or macOS, restrict the permissions first:
```
chmod 400 key-pair-name.pem
```
* Recommended remote access software:
    * Windows: MobaXterm
    * Linux: Remmina
    * macOS: Royal TSX
* VM Launch: Select your newly created key pair when deploying your Azure VM.
* Networking: Ensure SSH is allowed via the network security group, UFW allows SSH, and you have public or VPN access.

VM Status Checks:
-----------------
* Docs: https://learn.microsoft.com/en-us/azure/virtual-machines/boot-diagnostics
* Checking the status of your VM can reveal issues with your server.
* Azure Portal > Virtual Machines > check the Status column.
* Status: Running / Starting / Stopped / Deallocated / Failed.
* If the status shows failed, something is wrong with the VM. A reboot can sometimes resolve the issue.
* Troubleshoot: Select the VM > Help > Boot troubleshooting > Screenshot. The screenshot shows what the VM console is currently displaying.

Azure Service Health:
--------------------
* Docs: https://learn.microsoft.com/en-us/azure/service-health/overview
* Find out if there are any issues in your region, outages, etc.
* Azure Portal > Service Health. You can also check global outages here: https://status.azure.com/status/

VM Networking Topics:
--------------------
If you would like to learn more about networking related to Azure VMs, here are some quick links.

* Network Security Groups - https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview
* Virtual Networks - https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview
* Route Tables - https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-udr-overview
* NAT Gateway - https://learn.microsoft.com/en-us/azure/nat-gateway/nat-overview
* VPN Gateway - https://learn.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpngateways
* Public IPs - https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/public-ip-addresses
