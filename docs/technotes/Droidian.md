Droidian
========
"Droidian is a GNU/Linux distribution based on Debian for mobile devices. The goal of Droidian is to be able to run Debian on Android phones."


Devices:
--------
* Pixel 3a
* Many More

Pixel 3a Droidian Install:
--------------------------
* Install adb + Fastboot on Debian - https://dl.google.com/android/repository/platform-tools-latest-linux.zip
```
# Phone: About tap x7 > Enable useb debugging + OEM Unlock
# From your Debian device insta adb + Fastboot
sudo apt-get install -y android-tools-adb android-tools-fastboot
# Plug in device & Allow USB Debugging prompt
adb devices
adb reboot bootloader
fastboot flashing unlock
# Except Unluck Bootloader from Phone
# See Android 9 Stick Image 
cd sargo-pd2a.190115.029
unzip image-sargo-pd2a.190115.029.zip
bash flash-all.sh
```
* Save your APN - https://devices.droidian.org/#/devices/sargo ; https://apn.how/specs/google-pixel-3a
* Andoroid 9 Stock Image - https://developers.google.com/android/images
* Drodian Install Guide - https://devices.droidian.org/#/devices/sargo ; https://github.com/droidian-images/droidian 
* Drodian installer - https://github.com/droidian-releng/droidian-installer/releases/tag/0.0.5 ( Not working? )
* Droidian 99 - https://github.com/droidian-images/droidian/releases/tag/droidian%2F99

```
# Enable , dev , usb debugging, and oem ublick again.
# Need to accept via phone 
# Enter fastboot
wget https://images.droidian.org/droidian/nightly/arm64/google/image-fastboot-sargo.zip
unzip image-fastboot-sargo.zip
bash flash_all.sh
```

Plasma Mobile:
--------------
Mobian contains the plasma-mobile package that can be installed to turn Droidan Mobian to run Plasma-Moble, similar to customizing the desktop theme on regular linux. 

Android Emulator:
-----------------
"The AVD contains the full Android software stack, and it runs as if it were on a physical device." Could be utilized to develop android applications from the phone directly. 

* Issues: Experiemntal using as an emulated Android device.  
* Does it support Bliss OS? 

Waydorid:
---------
"A container-based approach to boot a full Android system on regular GNU/Linux systems running Wayland based desktop environments." 

* Issues: Uses older verison of Lineage, need to find out how to Upgrade the the latest version. 
* How do I install MicroG ? Do I instead use Lineage OS for MicroG?
* Does eSIM work? 

Qemu:
-----
Qemu can emulate ISOs , not sure the hardware capacity is enough . 

* Does it support BlissOS and how fast does it run?
* https://docs.blissos.org/installation/install-in-a-virtual-machine/install-in-qemu/

LXC:
---
Can install kubernetes / docker on LXC and run lite dev applications.

* Can it run lxc , install qemu , then install BlissOS ? 
* Build LXC images from your computer, save to github repo , and pull custom LXC continer to phone in one command. 

Steam:
-----
Can steam run on Drodian Mobian and if so , what games work?


References:
-----------
* https://droidian.org/
* https://mobian-project.org/
* https://plasma-mobile.org/get/
* https://source.android.com/docs/setup/create/avd
* https://lineage.microg.org/
* https://waydro.id/