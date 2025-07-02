Ventoy
======

Ventoy is an open-source tool that lets you easily create a multiboot USB drive by simply copying and pasting an ISO.

Install:
-------
```
# Download ventoy.
wget https://sourceforge.net/projects/ventoy/files/v1.1.05/ventoy-1.1.05-linux.tar.gz
# Extract it.
tar -xzf ventoy-1.1.05-linux.tar.gz
cd ventoy-1.1.05
# find your usb
lsblk
# Make the installation script executable
chmod +x Ventoy2Disk.sh
# Install ventoy to USb ( Caution make sure you use your usb path )
sudo ./Ventoy2Disk.sh -i /dev/sdc
# Copy over your ISO
sudo mkdir -p /media/$USER/Ventoy
sudo mount /dev/sdc1 /media/$USER/Ventoy
sudo cp /Downloads/*.iso /media/$USER/Ventoy/
# Can now test the multiboot USB device 
```

References:
-----------
* https://www.ventoy.net/en/index.html
