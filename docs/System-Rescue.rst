System Rescue
=====

     System Rescue is a multi-use utility live usb , built on Arch Linux.  

.. code-block:: console

  ###System Resue - Live USB###
  $ wget https://sourceforge.net/projects/systemrescuecd/files/sysresccd-x86/9.04/systemrescue-9.04-amd64.iso/download
  # Use Balena Etcher to make a live USB
  # Boot from computer - Research, models vary ( F2 or F12 ) 
  # Boot default : loads to terminal 
  $ startx
  # Connect to internet to install additonal packages
  $ pacman -Syu package-name-here

  ###System Rescue - Toolset###
  # Storage and disk partitioning
  * GParted
  * ddrescue 
  * fsarchiver and 
  * partclone 
  * fdisk, gdisk , cfdisks & fdisk
  * qemu-img & qemu-nbd 

  # Network tools
  * Network-Manager 
  * nmcli, ifconfig, ip, route, & dhclient
  * tcpdump
  * netcat and 
  * udpcast allow 
  * OpenVPN, WireGuard, & openconnect

  # File system tools
  * e2fsprogs, xfsprogs, & btrfs-progs
  * ntfs-3g 

  # Web Browsers and Internet
  * Firefox
  * curl 
  * wget 

  # Remote control
  * OpenSSH 
  * Remmina

  # Security
  * GnuPG
  * KeepassXC 
  * cryptsetup 
  * chntpw 

  # Recovery tools
  * testdisk 
  * photorec
  * whdd

  # Secure deletion
  * wipe & nwipe
  * shred 
  * mc
  * Thunar

  # Hardware information
  * lspci 
  * lsusb 
  * lscpu
  * hwinfo 

  # Hardware testing
  * memtest86 
  * memtester 
  * stress 

  # Boot loader and UEFI
  * Grub bootloader 
  * efibootmgr

  # Text editors
  * featherpad 
  * geany
  * vim 
  * nano 
  * joe 
  * ghex 
  * hexedit

  # Archival and file transfer
  * tar 
  * gzip, xz, zstd, lz4, &  bzip2
  * zip, unzip, & 7z 
  * rsync  
  * grsync 
  * rclone 

  # CD/DVD utilities
  * growisofs
  * cdrecord 
  * mkisofs 
  * udftools 

  # Scripting languages
  * bash 
  * Perl
  * Python 
  * Ruby 

  # Miscellaneous
  * flashrom 
  * nvme 


  ###References###
  https://www.system-rescue.org/