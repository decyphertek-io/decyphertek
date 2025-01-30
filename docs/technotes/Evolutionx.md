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
# Flash the Boot Image
fastboot flash boot boot.img
# Reboot to Recovery
fastboot reboot recovery
# Factory Reset (navigate in recovery)
# Select: Factory Reset → Format Data/Factory Reset and confirm
# Apply Update from ADB
# (navigate in recovery)
# Select: Apply Update → Apply from ADB
# Sideload the ROM
adb sideload rom.zip  # Replace "rom.zip" with the actual filename
# Optional: Reboot to Recovery for Add-ons (if needed)
adb reboot recovery
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