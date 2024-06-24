Cloud Init
=====

Cloud Init can be used by all Linux systems to customize builds in all cloud platforms. 

Install + Utilize
-----------------

     # Interactive
    sudo apt install cloud-init
    sudo dpkg-reconfigure cloud-init
    <OR>
    # Debian systems
    sudo vim 01_debian_cloud.cfg
    
    apt_preserve_sources_list: true
    manage_etc_hosts: true
    system_info:
      default_user:
        name: admin
        sudo: ALL=(ALL) NOPASSWD:ALL
        shell: /bin/bash
        lock_passwd: True
        gecos: Debian
        groups: [adm, audio, cdrom, dialout, dip, floppy, netdev, plugdev, sudo, video]
        sudo: ["ALL=(ALL) NOPASSWD:ALL"]
        shell: /bin/bash

    # Ubuntu Systems
    sudo vim /etc/cloud/cloud.cfg
    # Change ubuntu to the username you want. 
    system_info:
     # This will affect which distro class gets used
     distro: ubuntu
     # Default user name + that default users groups (if added/used)
     default_user:
       name: ubuntu
       lock_passwd: True
       gecos: Ubuntu

    sudo cloud-init clean --logs
    sudo cloud-init init --local
    sudo cloud-init init
    sudo cloud-init modules --mode=config
    sudo cloud-init modules --mode=final
    # On a server build , the ubuntu user still exists. Lets change that
    sudo pkill -KILL -u ubuntu
    sudo deluser ubuntu
    sudo rm -rf /home/ubuntu


References
----------

    https://cloud-init.io/
    https://www.digitalocean.com/community/tutorials/how-to-use-cloud-config-for-your-initial-server-setup
    https://stackoverflow.com/questions/23065673/how-to-re-run-cloud-init-without-reboot
