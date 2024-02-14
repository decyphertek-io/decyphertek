Qemu
====

An open Source Alternative to VirtualBox.

Install:
-------

    $ sudo apt update
    $ sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager -y
    $ sudo virsh net-autostart default
    # Virtual machine manager > create new machine > Select local install media ( ISO ) > Set memory, CPU , & Storage > Finish

References:
-----------

https://itslinuxfoss.com/install-setup-qemu-debian-12/