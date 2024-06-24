Debian Medical is part of Debian Pure Blends and provides an all in one distro geared
towards the medical industry. 

Install
-------

    # Debian 11 Server
    sudo apt update
    sudo apt install med-all task-xfce-desktop xrdp
    sudo systemctl get-default
    sudo systemctl set-default graphical.target
    # Adjust RDP color settings and resolution settings if needed via your chosen RDP application.
    # The color quality setting can slow down or speed up the RDP connection. 
    sudo vim /etc/polkit-1/localauthority/50-local.d/allow-color.pkla
    [Allow Colord all Users]
    Identity=unix-user:*
    Action=org.freedesktop.color-manager.create-device;org.freedesktop.color-manager.create-profile;org.freedesktop.color-manager.delete-device;org.freedesktop.color-manager.delete-profile;org.freedesktop.color-manager.modify-device;org.freedesktop.color-manager.modify-profile
    ResultAny=no
    ResultInactive=no
    ResultActive=yes
    sudo vim /etc/polkit-1/localauthority/50-local.d/update-color.pkla
    
    [Allow Package Management all Users]
    Identity=unix-user:*
    Action=org.freedesktop.packagekit.system-sources-refresh
    ResultAny=yes
    ResultInactive=yes
    ResultActive=yes
    
    # Need to have a passwd set to be able to RDP into system
    sudo passwd $USER
    # Allow RDP access to firewall and Security group
    sudo ufw allow 3389/tcp 
    sudo reboot
    # Use Mobaxterm , Remmina , or Royal TS

References
----------

    https://blends.debian.org/blends/ch04.html#debian-med
    https://wiki.debian.org/DebianMed
    https://linux.die.net/man/8/xrdp