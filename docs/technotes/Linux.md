Linux-101
=====

Linux is an open source operating system. Learn how to navigate the terminal and do some basic tasks. 

Add user
--------

     # This will add a user to the following locations: /etc/passwd, /etc/shadow, /etc/group and /etc/gshadow
     # The -m option after useradd, will make a home directory.
     $ sudo useradd -m username
     $ sudo passwd username
     # Add to sudo group
     $ sudo usermod -aG sudo username
     # No sudo password for username
     $ sudo visudo
     username ALL=(ALL) NOPASSWD:ALL
     # Fix bash shell not showing username and hostname
     $ sudo chsh -s /bin/bash username

Remove a user
-------------

     # Make sure user is logged out
     $ sudo pkill -KILL -u username
     $ sudo deluser username
     # Manually remove from sudo no password
     $ sudo visudo
     # Delete and save
     username ALL=(ALL) NOPASSWD:ALL

Change Hostname
----------------

     $ sudo hostnamectl set-hostname "decyphertek"
     $ sudo su -c "echo '127.0.1.1 decyphertek' >> /etc/hosts"
     $ hostnamectl
     # Logout 

History
-------

     # Manually Change History
     $ vim ~/.bash_history
     # dd or change / add 
     $ exit
     # log back in
     $ history

System Info
-----------

     $ sudo apt install -y neofetch
     $ neofetch

Network Info
-------------

     # Get your ip address
     $ sudo apt install net-tools
     $ ifconfig
     # See listening ports 
     $ netstat -tuna

apt-key deprecated
-------------------

     $ sudo apt-key list
     # Replace 3213339E with the last x4 of the pub. You can rename the .gpg if using trusted.gpg to something relevant. 
     $ sudo apt-key export 3213339E | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/namehere.gpg
     # A quick way is to just move the key
     $ sudo mv /etc/apt/trusted.gpg /etc/apt/trusted.gpg.d/trusted.gpg

Bluetooth
---------

     # Minimal Xubuntu 22.04 Minimal Desktop install doesnt have Bluetooth software installed.
     # PulseAudio Option 
     $ sudo apt install -y blueman bluez* pulseaudio pulseaudio-module-bluetooth pulseaudio-equalizer xfce4-pulseaudio-plugin ubuntu-restricted-extras linux-firmware firmware-sof-signed
     $ sudo systemctl daemon-reload
     $ sudo systemctl stop bluetooth. service
     $ sudo systemctl unmask bluetooth.service
     $ sudo systemctl start bluetooth.service
     $ sudo systemctl enable bluetooth
     $ sudo systemctl mask bluetooth.service 
     $ sudo rmmod btusb
     $ sudo modprobe btusb
     $ sudo rfkill unblock all
     # Purge Pipewire Conflicts , if any with pulsewire
     $ sudo apt purge -y pipewire* libspa-0.2-bluetooth
     $ sudo apt autoremove
     # reboot system
     $ pactl info
     $ pulseaudio -k
     $ pulseaudio --start

     # PipeWire Option - Xfce desktop bluetooth issues . 
     $ sudo add-apt-repository ppa:pipewire-debian/pipewire-upstream
     $ sudo apt update && sudo apt install -y pipewire libspa-0.2-bluetooth pipewire-audio-client-libraries pulseaudio-module-bluetooth ubuntu-restricted-extras linux-firmware firmware-sof-signed
     $ sudo apt purge pulseaudio*
     # Reboot system
     $ pactl info
    
ACL
----

     $ sudo apt-get install nfs4-acl-tools acl
     # Read , Write , & Execute access to a single user
     $ sudo setfacl -m u:username:rwx folder/
     # Add recursive permissions 
     $ sudo setfacl -m u:username:rwx -R folder/ 
     # Read , Write , & Execute access to All Users in a group
     $ sudo setfacl -m g:groupname:rwx folder/
     # You can set which permisisons you want the user or group to have.
     $ sudo getfacl folder/
     # Revoke user & group access
     $ sudo setfacl -x u:username,g:groupname folder/
     
Enable AWS Workspace
--------------------

     # To enable access for your Linux system, please follow these steps :
     1. AWS Console > WorkSpaces > Directories > Select your directory > Scroll down: Other Platforms > Edit > Select Linux
   
References
----------

     https://linuxize.com/post/how-to-create-users-in-linux-using-the-useradd-command/
     https://www.systutorials.com/docs/linux/man/8-deluser/
     https://www.cyberciti.biz/faq/linux-logout-user-howto/
     https://askubuntu.com/questions/388440/why-is-there-no-name-showing-at-the-command-line
     https://www.howtogeek.com/197934/how-to-change-your-hostname-computer-name-on-ubuntu-linux/
     https://linoxide.com/linux-set-access-control-list-using-setfacl-and-getfacl-commands/
     https://linuxhint.com/change-hostname-ubuntu-permanently/
     https://askubuntu.com/questions/1339765/replacing-pulseaudio-with-pipewire-in-ubuntu-20-04


