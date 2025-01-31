EvolutionX:
===========
Can run Android 15 on phones no longer supported by google. 

Install:
--------
```
# From your Debian device install adb + Fastboot
sudo apt-get install -y android-tools-adb android-tools-fastboot
# Plug in device & Allow USB Debugging prompt
adb kill-server && adb start-server
adb devices
adb reboot bootloader
# Except Unlock Bootloader from Phone
fastboot flashing unlock
# Reboot to Bootloader
adb reboot bootloader
# Download the boot.img and rom.zip from EvolutionX downloads page for your device
https://evolution-x.org/downloads
# Pixel 3a Sargo Example:
wget https://master.dl.sourceforge.net/project/evolution-x/sargo/15/boot/boot.img
wget https://pilotfiber.dl.sourceforge.net/project/evolution-x/sargo/15/EvolutionX-15.0-20250127-sargo-10.2-Official.zip
# Flash the Boot Image
fastboot flash boot boot.img
# Reboot to Recovery
fastboot reboot recovery
# Select: Factory Reset > Format Data/Factory Reset and confirm
# Select: Apply Update > Apply from ADB
adb sideload EvolutionX-15.0-20250127-sargo-10.2-Official.zip
# Reboot to System
adb reboot system
```

Degoogle w/ universal-android-debloater-next-generation:
---------------------------------------------------------
```
wget https://github.com/Universal-Debloater-Alliance/universal-android-debloater-next-generation/releases/download/v1.1.0/uad-ng-linux
chmod + x uad-ng-linux
./uad-ng-linux
```

References:
----------
* https://evolution-x.org/downloads