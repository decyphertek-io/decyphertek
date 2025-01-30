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
```

Flatpak Mobile Apps:
-------------------
* https://flathub.org/apps/collection/mobile/1
```
# Flatpak is already installed
# This will make it easier to install Flatpaks
flatpak install warehouse
# Flatpaks is tied to the gnome store, except found it slow. 
```

Waydroid:
---------
* Settings > Waydroid > install 

Dev in Progress: Fixing arm apps that are not mobile friendly:
--------------------------------------------------
```
#Organic Map example
flatpak install -y flathub org.organicmaps.Desktop

# 3. Mobile optimization
flatpak override --user org.organicmaps.Desktop \
  --env=GDK_BACKEND=wayland \
  --env=QT_QPA_PLATFORM=wayland \
  --socket=wayland \          
  --device=input \            
  --env=GDK_DPI_SCALE=0.8 \  
  --env=QT_SCALE_FACTOR=1.5  

# 4. Create launcher 
cat > ~/.local/share/applications/org.organicmaps.Desktop.desktop << 'EOL'
[Desktop Entry]
Name=Organic Maps
Exec=flatpak run org.organicmaps.Desktop
Icon=org.organicmaps.Desktop
Categories=Navigation;Mobile;
Terminal=false
Type=Application
X-GNOME-UsesNotifications=true
EOL

# 5. Finalize 
update-desktop-database ~/.local/share/applications
systemctl --user restart phosh 

# PIA Example
# 1. Download and install
wget https://installers.privateinternetaccess.com/download/pia-linux-3.6.1-08339.run
chmod +x pia-linux-*.run
sudo ./pia-linux-*.run

# 2. Create mobile-friendly launcher
cat > ~/.local/share/applications/pia.desktop << 'EOL'
[Desktop Entry]
Name=PIA VPN
Exec=env GDK_DPI_SCALE=0.8 QT_SCALE_FACTOR=1.5 /opt/pia/pia-client
Icon=/opt/pia/pia.png
Categories=Network;Mobile;
Terminal=false
Type=Application
X-Purism-FormFactor=Mobile
StartupWMClass=pia-ui
EOL

# 3. Set permissions
sudo chmod 644 ~/.local/share/applications/pia.desktop

# 4. Mobile environment
echo "export GDK_DPI_SCALE=0.8" >> ~/.profile
echo "export QT_SCALE_FACTOR=1.5" >> ~/.profile

# 5. Finalize
update-desktop-database ~/.local/share/applications
systemctl --user restart phosh
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