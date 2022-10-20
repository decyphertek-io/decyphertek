Rport
======

"RPort - an all-in-one remote management suite for heterogeneous environments. RPort addresses three basic needs of a sysadmin: "

Ports
-----

    # Allow Ports on AWS Security Group:
    port 22/tcp SSH 
    port 0-65535/tcp ICMP 
    port 80/tcp HTTP
    port 443/tcp HTTPS 
    port 20000-30000/tcp custom

Install
--------

    $ sudo apt update
    $ curl https://get.rport.io -o rport-install.sh
    $ sudo bash rport-install.sh
    # See output on terminal , user & pass. 
    # Edit configs
    $ sudo vim /etc/rport/rportd.conf


References
----------

    https://rport.io/
    https://kb.rport.io/install-the-rport-server/install-rport-on-any-virgin-cloud-vm
    https://kb.rport.io/install-the-rport-server
    https://kb.rport.io/install-the-rport-server/install-on-aws-ec2
    https://kb.rport.io/install-the-rport-server/enable-two-factor-authentication