GNS3
====

Network Simulator. 

Ubuntu Install:
-------

    # Ubuntu install:
    sudo add-apt-repository ppa:gns3/ppa
    sudo apt update                                
    sudo apt install gns3-gui gns3-server
    # “sudo usermod -aG group user_name” 
    ubridge libvirt kvm wireshark docker

    # Install Docker:
    $ curl -fsSL https://raw.githubusercontent.com/decyphertek-io/bash/main/docker.sh | bash

Debian 12 install:
------------------

    # GNS3
    sudo apt install -y python3-pip python3-pyqt5 python3-pyqt5.qtsvg python3-pyqt5.qtwebsockets qemu-kvm qemu-utils libvirt-clients libvirt-daemon-system virtinst \
    wireshark xtightvncviewer apt-transport-https ca-certificates curl gnupg2 software-properties-common python3-pyqt5.qtwebengine vpcs mtools bridge-utils libpcap-dev 
    sudo pip3 install gns3-server --break-system-packages
    sudo pip3 install gns3-gui --break-system-packages

    # GNS3 Ubridge Install 
    git clone https://github.com/GNS3/ubridge.git && cd ubridge
    make && sudo make install

    # GNS3 Set permissions
    sudo addgroup ubridge
    sudo usermod -aG ubridge,libvirt,kvm,wireshark,docker $(whoami)

    # Be sure to modify gns3_server.conf to point to /usr/local/bin/ubridge
    sudo vim /home/$USER/.config/GNS3/2.2/gns3_server.conf
    ubridge_path = /usr/local/bin/ubridge

References:
-----------

    https://docs.gns3.com/docs/getting-started/installation/linux