Waydroid
========

Waydroid is a container-based solution that enables users to run a full Android system on Linux, offering a seamless experience by integrating Android apps directly into the Linux desktop / Phone . 

Devices:
--------
* Arch Linux
* Ubuntu/Debian
* Postmarket OS
* Zorin OS
* Sailfish OS
* Fedora
* Opensuse
* Kiss Linux
* Void Linux
* NixOS

Ubuntu/Debian Install:
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

Issues:
-------
* Debian 12 XFCE uses x11 and not wayland , getting this error.
```
waydroid session start
[15:53:09] WAYLAND_DISPLAY is not set, defaulting to "wayland-0"
[15:53:09] Wayland socket '/run/user/1000/wayland-0' doesn't exist; are you running a Wayland compositor?
```
* It uses an old version of LineageOS 18 , not the recent version 21. 

References:
-----------
* https://docs.waydro.id/usage/install-on-desktops
* https://waydro.id/#install