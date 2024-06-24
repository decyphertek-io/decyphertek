FreedomBox
===========

Take back your online freedom. Has a multitude of applications as a one click install.

Install
--------

    sudo apt update
    sudo DEBIAN_FRONTEND=noninteractive apt-get install freedombox
    # Secret Key 
    cat /var/lib/plinth/firstboot-wizard-secret
    sudo vim /etc/network/interfaces
    auto lo 
    iface lo inet loopback

Optional : Network Configuration Commands
------------------------------------------

    nmcli con mod "Ethernet connection 1" \ ipv4.addresses A.A.A.A/X \ 
    ipv4.gateway G.G.G.G \ 
    ipv4.dns N.N.N.N \ 
    ipv4.dns-search somedomain.com \ ipv4.method "manual" \ 
    ipv4.ignore-auto-dns yes \ 
    ipv6.method ignore


References
-----------

    https://wiki.debian.org/FreedomBox
    https://wiki.debian.org/FreedomBox/Manual#FreedomBox.2FHardware.2FDebian.Debian