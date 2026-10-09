GCP Basics
----------

If you're new to GCP and need a quick reference guide, this is a good place to start. [GCP Marketplace: Decyphertek ](https://console.cloud.google.com/marketplace/browse?filter=partner:decyphertek.io)

SSH Keys:
--------
* Add a key pair for secure SSH access to your Compute Engine instances.
* Docs: https://cloud.google.com/compute/docs/connect/add-ssh-keys
* GCP Console > Compute Engine > Settings > Metadata > SSH Keys > Edit > Add SSH key ( paste your public key ).
* Or use SSH-in-browser: GCP Console > Compute Engine > VM Instances > SSH. GCP can auto-generate SSH keys for you.
* You can also create a key pair on Linux or macOS:
```
ssh-keygen -t rsa -b 4096
ssh-keygen -t ed25519
```
* Permissions: If you use a .pem key on Linux or macOS, restrict the permissions first:
```
chmod 400 key-pair-name.pem
```
* Recommended remote access software:
    * Windows: MobaXterm
    * Linux: Remmina
    * macOS: Royal TSX
* VM Launch: Project-wide metadata SSH keys are available to every instance in the project. You can also add keys to a single instance.
* Networking: Ensure SSH is allowed via the VPC firewall rules, UFW allows SSH, and you have public or VPN access.

VM Status Checks:
-----------------
* Docs: https://cloud.google.com/compute/docs/instances/instance-lifecycle
* Checking the status of your instance can reveal issues with your server.
* GCP Console > Compute Engine > VM Instances > check the Status column.
* Status: Provisioning / Staging / Running / Stopped / Terminated.
* If the instance does not show a green check mark, something is wrong with the instance. A reboot can sometimes resolve the issue.
* Troubleshoot: Select the instance > Logs ( serial port ) to see the boot output: https://cloud.google.com/compute/docs/troubleshooting/viewing-serial-port-output

GCP Health Dashboard:
--------------------
* Docs: https://cloud.google.com/service-health/docs/overview
* Find out if there are any issues in your region, outages, etc.
* GCP Console > Personalized Service Health. You can also check global outages here: https://status.cloud.google.com/

VM Networking Topics:
--------------------
If you would like to learn more about networking related to GCP instances, here are some quick links.

* Firewall Rules - https://cloud.google.com/vpc/docs/firewalls
* VPC - https://cloud.google.com/vpc/docs/overview
* Routes - https://cloud.google.com/vpc/docs/routes
* Cloud NAT - https://cloud.google.com/nat/docs/overview
* Cloud VPN - https://cloud.google.com/network-connectivity/docs/vpn/concepts/overview
* External IPs - https://cloud.google.com/compute/docs/ip-addresses
