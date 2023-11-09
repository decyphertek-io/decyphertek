LXD - Canonicals improved LXC
==============================

Canonicals spin on LXC. Incus is a fork of LXD.  

Install LXD:
-----------

    $ sudo snap install --stable lxd
    $ sudo snap refresh --stable lxd
    $ sudo snap set lxd ui.enable=true
    $ sudo systemctl reload snap.lxd.daemon
    https://ip-of-server:8443