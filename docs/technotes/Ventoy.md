Ventoy
======

Ventoy is an open-source tool that lets you easily create a multiboot USB drive by simply copying and pasting an ISO.

Install:
-------

    # Download ventoy.
    wget https://sourceforge.net/projects/ventoy/files/v1.0.99
    # Extract it.
    tar -xzf ventoy.tar.gz
    cd ventoy-1.0.99
    # find your usb
    lsblk
    # Make the installation script executable
    chmod +x Ventoy2Disk.sh
    # Install ventoy to USb ( Caution make sure you use your usb path )
    sudo ./Ventoy2Disk.sh -i /dev/sdc
    # Copy over your ISO
    cp /Downloads/debian.iso /media/$USER/Ventoy/

References:
-----------

    https://www.ventoy.net/en/index.html
