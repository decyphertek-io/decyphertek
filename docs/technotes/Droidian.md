Droidian
========
"Droidian is a GNU/Linux distribution based on Debian for mobile devices. The goal of Droidian is to be able to run Debian on Android phones."

Devices:
--------
* Pixel 3a
* Pinephone
* Fairphone

Pixel 3a Droidian Install:
--------------------------
```
# Phone: About > tap Build Number x7 # System > Dev options > Enable usb debugging + OEM Unlock
# From your Debian device install adb + Fastboot
sudo apt-get install -y android-tools-adb android-tools-fastboot
# Plug in device & Allow USB Debugging prompt
adb kill-server && adb start-server
adb devices
adb reboot bootloader
# Except Unlock Bootloader from Phone
fastboot flashing unlock
wget https://dl.google.com/dl/android/aosp/sargo-pd2a.190115.029-factory-b05c97da.zip
unzip image-sargo-pd2a.190115.029.zip
cd  sargo-pd2a.190115.029
bash flash-all.sh
# Enable , dev , usb debugging, and oem unlock again. Need to accept via phone again.
# Enter fastboot
wget https://github.com/droidian-images/droidian/releases/download/nightly/droidian-OFFICIAL-phosh-phone-google_sargo-api28-arm64-next_20250129.zip
unzip droidian-OFFICIAL-phosh-phone-google_sargo-api28-arm64-next_20250129.zip
bash flash_all.sh
login: 1234
# Set encyrption > Settings > Encryption > Reboot > Be patient screen turns black after login 30-90 sec.
# Change login password from 1234 , Open terminal:
sudo passwd droidian 
# Number pin code is the easiest way, so you can login via pin.
# USB Settings: Settings > USB > None , File Transfer , Networking ( If enabled can access droidian with no authentication )
```

Flatpak Mobile Apps:
-------------------
* https://flathub.org/apps/collection/mobile/1
* Flatpak is already installed
* You can install via Gnome App Store and check if its mobile friendly 

Waydroid:
---------
* Settings > Waydroid > install 

Issues:
-------
* GPS Not working
* Esim not working
* Waydroid doesnt work with VPN on Drodian
* Flatpak apps even suppose to work on mobile, are glitchy. 

References:
-----------
* https://droidian.org/
* https://mobian-project.org/
* https://waydro.id/
* Save your APN - https://devices.droidian.org/#/devices/sargo ; https://apn.how/specs/google-pixel-3a
* Andoroid 9 Stock Image - https://developers.google.com/android/images
* Drodian Install Guide - https://devices.droidian.org/#/devices/sargo ; https://github.com/droidian-images/droidian 
* Drodian installer - https://github.com/droidian-releng/droidian-installer/releases/tag/0.0.5 ( Not working? )
* Droidian 99 - https://github.com/droidian-images/droidian/releases/tag/droidian%2F99