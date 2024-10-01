Waydroid
========

Waydroid is a container-based solution that enables users to run a full Android system on Linux, offering a seamless experience by integrating Android apps directly into the Linux desktop / Phone . 

Debian Install:
---------------
```
sudo apt install curl ca-certificates -y
curl https://repo.waydro.id | sudo bash
sudo apt install waydroid -y
sudo waydroid init
sudo waydroid container start
# Open A new terminal and run :
waydroid session start
# Systemd Enable:
sudo systemctl enable --now waydroid-container
# Optional: Full Screen
waydroid show-full-ui
# Install APK;
waydroid app install appname.apk
```

References:
-----------
* https://docs.waydro.id/usage/install-on-desktops
* https://waydro.id/#install