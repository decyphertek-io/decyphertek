Syslinux
=====

     Syslinux provides the terminal way of setting up a Multiboot usb.

.. code-block:: console

     ###Syslinux - Multiboot USB###
     # Format USB to Fat32 using Gparted or fdisk
     $ sudo apt install Syslinux
     # find where your usb is mounted
     $ lsblk
     $ sudo syslinux -s -i /dev/sda1
     $ sudo dd conv=notrunc bs=440 count=1 if=mbr.bin of=/dev/sda 
     $ sudo parted /dev/sda set 1 boot on
     # Find the mount point
     # lsblk
     $ cd /media/$USER/
     $ ls
     # you should see the usb mounted cd to it
     $ mkdir -p boot/syslinux
     $ cp /usr/lib/syslinux/bios/*.c32 boot/syslinux/
     
     ###References###
     https://wiki.syslinux.org/wiki/index.php?title=HowTos#How_to_Create_a_Bootable_USB:_For_Linux
