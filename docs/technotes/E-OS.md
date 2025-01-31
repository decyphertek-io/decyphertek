e/OS:
====
De-googled Android with MicroG and privacy features. Supports legacy and modern devices. 

Install:
--------
```
# From your Debian device install adb + Fastboot
sudo apt-get install -y android-tools-adb android-tools-fastboot
# Phone > Settings > About Phone > Tap Build number x7 times 
# Phone > Settings > System > Advanced > Select Developer Options > Enable OEM Unlocking and USB Debugging
# Plug in device to the computer & Allow USB Debugging prompt
adb kill-server && adb start-server
adb devices
adb reboot bootloader
# Except Unlock Bootloader from Phone
fastboot flashing unlock
# Reboot to Bootloader
adb reboot bootloader
# Upgrade to Android 12 - Pixel 3a Sargo Example:
wget https://dl.google.com/dl/android/aosp/sargo-sp2a.220505.008-factory-071e368a.zip
unzip sargo-sp2a.220505.008-factory-071e368a.zip
cd sargo-sp2a.220505.008-factory-071e368a
bash flash-all.sh
# Boot into android 12 & Do the same unlocking process mentioned above.
# Get the device images and ROM. ( Some devices support Easy installer )
https://doc.e.foundation/devices
# EX: Pixel 3a Sargo ( Manual install using adb )
https://doc.e.foundation/devices/sargo/community
https://doc.e.foundation/devices/sargo/install
# Dowload the recovery Image ( make sure version matches)
wget https://images.ecloud.global/community/sargo/recovery-e-2.7-u-20250111460593-community-sargo.img
# Download the Rom.zip ( make sure verison matches )
wget https://images.ecloud.global/community/sargo/e-2.7-u-20250111460593-community-sargo.zip
fastboot flash boot recovery-e-2.7-u-20250111460593-community-sargo.img
* Use volume buttons > Select Recovery mode w/ power button
* Select > Factory reset > Format data / Factory reset w/ power button > format data
* Back a screen > Apply Update > Apply from ADB 
adb sideload e-2.7-u-20250111460593-community-sargo.zip 
# Reboot when finished
# Optional: Relock Bootloader ( Will erase all data , may brick your device )
* Follow same procedure to enable usb and access fastboot
fastboot flashing lock
```

References:
----------
* https://e.foundation/e-os/