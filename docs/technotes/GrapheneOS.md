GrapheneOS:
==========
Privacy-focused, hardened Android for Google Pixel devices. No Google services, verified boot enforced.

Install:
--------
```
# Prerequisites: 2GB RAM, 32GB free storage, USB-C cable, carrier-unlocked Pixel device
# Phone > Settings > About phone > Tap Build number x7 ( enable Developer options )
# Phone > Settings > System > Developer options > Toggle OEM unlocking ON

# Install fastboot on Debian
sudo apt install android-sdk-platform-tools-common libarchive-tools openssh-client
curl -O https://dl.google.com/android/repository/platform-tools_r35.0.2-linux.zip
echo 'acfdcccb123a8718c46c46c059b2f621140194e5ec1ac9d81715be3d6ab6cd0a  platform-tools_r35.0.2-linux.zip' | sha256sum -c
bsdtar xvf platform-tools_r35.0.2-linux.zip
export PATH="$PWD/platform-tools:$PATH"
fastboot --version  # Must be >= 35.0.1

# Stop fwupd to prevent USB conflicts
sudo systemctl stop fwupd.service

# Boot phone into Fastboot mode
adb kill-server && adb start-server
adb devices
adb reboot bootloader
fastboot flashing unlock  
# Volume up & select unlock bootloader

# Download & verify factory images
# https://releases.grapheneos.org/
# Device codenames:
#   Pixel 10a         = stallion
#   Pixel 10 Pro Fold = rango
#   Pixel 10 Pro XL   = mustang
#   Pixel 10 Pro      = blazer
#   Pixel 10          = frankel
#   Pixel 9a          = tegu
#   Pixel 9 Pro Fold  = comet
#   Pixel 9 Pro XL    = komodo
#   Pixel 9 Pro       = caiman
#   Pixel 9           = tokay
#   Pixel 8a          = akita
#   Pixel 8 Pro       = husky
#   Pixel 8           = shiba
#   Pixel Fold        = felix
#   Pixel Tablet      = tangorpro
#   Pixel 7a          = lynx
#   Pixel 7 Pro       = cheetah
#   Pixel 7           = panther
#   Pixel 6a          = bluejay
#   Pixel 6 Pro       = raven
#   Pixel 6           = oriole
# Please verify the code name and device is correct before installing. 
curl -O https://releases.grapheneos.org/allowed_signers
curl -O https://releases.grapheneos.org/DEVICE_NAME-install-VERSION.zip
curl -O https://releases.grapheneos.org/DEVICE_NAME-install-VERSION.zip.sig
ssh-keygen -Y verify -f allowed_signers -I contact@grapheneos.org -n "factory images" \
  -s DEVICE_NAME-install-VERSION.zip.sig < DEVICE_NAME-install-VERSION.zip
# Expected output: Good "factory images" signature for contact@grapheneos.org
# Flash GrapheneOS
bsdtar xvf DEVICE_NAME-install-VERSION.zip
cd DEVICE_NAME-install-VERSION
bash flash-all.sh
# Do not touch the device until script completes

# Pixel 7a (lynx) example:
curl -O https://releases.grapheneos.org/lynx-install-2026040800.zip
curl -O https://releases.grapheneos.org/lynx-install-2026040800.zip.sig
ssh-keygen -Y verify -f allowed_signers -I contact@grapheneos.org -n "factory images" \
  -s lynx-install-2026040800.zip.sig < lynx-install-2026040800.zip
# Expected output: Good "factory images" signature for contact@grapheneos.org
# Flash GrapheneOS
bsdtar xvf lynx-install-2026040800.zip
cd lynx-install-2026040800
bash flash-all.sh
# Do not touch the device until script completes

# Lock the bootloader ( required for verified boot )
fastboot flashing lock  # Confirm on device; this wipes data again

# Power on: press power button with "Start" selected in bootloader menu
# First setup: leave OEM unlocking DISABLED ( default checked )

# Optional: verify install boot key hash on yellow boot screen
# Compare against: https://grapheneos.org/install/cli#verified-boot-key-hash
# EX Pixel 7a: 508d75dea10c5cbc3e7632260fc0b59f6055a8a49dd84e693b6d8899edbb01e4

# Optional: revert to stock OS ( erase GrapheneOS verified boot key first )
fastboot erase avb_custom_key
# Then flash stock factory images using same process above
```

References:
-----------
* https://grapheneos.org/install/cli
* https://releases.grapheneos.org/
