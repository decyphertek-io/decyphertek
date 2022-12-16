Debian Medical is part of Debian Pure Blends and provides an all in one distro geared
towards the medical industry. 

Install
-------

    $ sudo apt update
    $ sudo apt install med-all task-xfce-desktop xrdp
    $ sudo systemctl get-default
    $ sudo systemctl set-default graphical.target
    $ sudo vim sudo vim /etc/polkit-1/localauthority/50-local.d/color.pkla
    [Allow Colord all Users]
    Identity=unix-user:*
    Action=org.freedesktop.color-manager.create-device;org.freedesktop.color-manager.create-profile;org.freedesktop.color-manager.delete-device;org.freedesktop.color-manager.delete-profile;org.freedesktop.color-manager.modify-device;org.freedesktop.color-manager.modify-profile
    ResultAny=no
    ResultInactive=no
    ResultActive=yes
    # Need to have a passwd set to be able to RDP into system
    $ sudo passwd $USER
    # Allow RDP access to firewall and Security group
    $ sudo ufw allow 3389/tcp 
    $ sudo reboot
    # Use Mobaxterm , Reminna , or Whatever Mac uses to RDP. 

References
----------

    https://blends.debian.org/blends/ch04.html#debian-med
    https://wiki.debian.org/DebianMed
    https://linux.die.net/man/8/xrdp