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
wget https://images.droidian.org/droidian/nightly/arm64/google/image-fastboot-sargo.zip
unzip image-fastboot-sargo.zip
bash flash_all.sh
login: 1234
# Set encyrption > Settings > Encryption > Reboot > Be patient screen turns black after login 30 sec.
# Change login password from 1234 , Open terminal:
sudo passwd droidian 
# Number pin code is the easiest way, so you can login via pin.
# To relock the bootloader
* Power off > Power + Volume down buttons
fastboot flashing lock
```

Flatpak Mobile Apps:
-------------------
* https://flathub.org/apps/collection/mobile/1
```
# Install Flatpak 
sudo apt update
sudo apt install flatpak
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
# Search for support arm architecture
flatpak --supported-arches
flatpak search --columns=name,description,application "" | grep -i mobile
flatpak install --arch=aarch64 org.appname
```

References:
-----------
* https://droidian.org/
* https://mobian-project.org/
* https://plasma-mobile.org/get/
* https://source.android.com/docs/setup/create/avd
* https://lineage.microg.org/
* https://waydro.id/
* Save your APN - https://devices.droidian.org/#/devices/sargo ; https://apn.how/specs/google-pixel-3a
* Andoroid 9 Stock Image - https://developers.google.com/android/images
* Drodian Install Guide - https://devices.droidian.org/#/devices/sargo ; https://github.com/droidian-images/droidian 
* Drodian installer - https://github.com/droidian-releng/droidian-installer/releases/tag/0.0.5 ( Not working? )
* Droidian 99 - https://github.com/droidian-images/droidian/releases/tag/droidian%2F99