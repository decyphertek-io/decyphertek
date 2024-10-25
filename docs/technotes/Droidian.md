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
fastboot --slot=other flash bootloader bootloader-sargo-b4s4-0.1-5262905.img
fastboot flash system system.img  
fastboot flash recovery recovery.img  
fastboot flash userdata userdata.img  
fastboot set_active other
fastboot reboot bootloader
fastboot set_active other
fastboot reboot bootloader
fastboot reboot
```
* Save your APN - https://devices.droidian.org/#/devices/sargo ; https://apn.how/specs/google-pixel-3a
* Andoroid 9 Stock Image - https://developers.google.com/android/images
* Drodian Install Guide - https://devices.droidian.org/#/devices/sargo ; https://github.com/droidian-images/droidian 
* Drodian installer - https://github.com/droidian-releng/droidian-installer/releases/tag/0.0.5
* Droidian 99 - https://github.com/droidian-images/droidian/releases/tag/droidian%2F99

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