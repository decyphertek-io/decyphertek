LXD 
===

LXD improves upon LXC , making it easy to install and manage.  

Install LXD:
-----------
```
sudo apt update
sudo apt install -y lxd
sudo usermod -aG lxd "$USER"
sudo lxd init --minimal
sudo lxc remote set-url images https://images.lxd.canonical.com
sudo lxc launch images:debian/12 decyphertek
sudo lxc image list
sudo systemctl enable lxd
sudo systemctl start lxd
sudo exec decyphertek -- /bin/bash
# Save an Image
sudo lxc stop decyphertek
sudo lxc publish decyphertek --alias decyphertek-published
sudo lxc image export decyphertek-published decyphertek-prod
# Deploy the exported image
sudo lxc image import decyphertek-prod.tar.gz --alias decyphertek-prod
sudo lxc launch decyphertek-prod decyphertek-prod-live
# To route traffic from LXC to localhost, need to get the image IP
sudo lxc image list
# Then you can add it to this command
sudo lxc config device add decyphertek-prod APPNAME proxy listen=tcp:127.0.0.1:443 connect=tcp:YOUR_LXC_IP:443
```

References:
-----------
* https://wiki.debian.org/LXD