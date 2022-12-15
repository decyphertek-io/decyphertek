Zentyal
=======

Linux Active Directory alternative and can act as a secondary domain controller. It has many mdoules 
to choose from , including AD , DNS , Email , Firewall, Jabber, and Intrusion Preventation System. 

Install 
--------

    # Zentyal Development Edition 7.0.5
    $ sudo vim /etc/apt/sources.list.d/zentyal.list
    $ deb http://packages.zentyal.org/zentyal 7.0 main extra
    $ wget -q http://keys.zentyal.org/zentyal-7.0-packages-org.asc -O- | sudo apt-key add -
    $ sudo apt update && sudo apt install zentyal
    # Select port 8443 
    $ sudo passwd $USER
    # https://ip-of-server:8443
    Follow setup instructions
    # If you want select Intrusion Prevention system, you need the following repo. 
    $ sudo add-apt-repository ppa:oisf/suricata-stable && sudo apt update
    # The save changes screen when done doesnt change to another screen, it stops at  Saving webadmin module
    # Open up a new window and manually save, when 2/2 100% , then refresh the page.  The original page will reflect the save. 
    $ sudo reboot

Ports & Protocols
-----------------
    
    # The following port list is an example if you install every module that Zentyal has, from firewall, to email, to Jabber. 
    # Make sure to allow ports and protocols via UFW or if you installed the firewall , via that. 
    # If you install Zentyal Firewall , it disables UFW . There disables firewall security , until you set it on Zentyal. Nmap scan confirms. 
    21/tcp ftp
    22/tcp ssh
    25/tcp smtp
    88/tcp kerberos-sec # Kerberos authentication
    110/tcp pop3
    135/tcp msrpc # domain controllers-to-domain controller and client to domain controller operations.
    139/tcp netbios-ssn # File Replication Service between domain controllers.
    143/tcp imap
    389/tcp LDAP
    443/tcp https
    445/tcp microsoft-ds # File Replication Service
    464/tcp kpasswd5 # Kerberos Password Change
    465/tcp smtps
    587/tcp submission
    993/tcp imaps
    995/tcp pop3s
    5222/tcp xmpp-client # Jabber
    8443/tcp https-alt
    49152/tcp dynamic applications
    49153/tcp dynamic applications
    49154/tcp dynamic applications

UFW host Firewall
-----------------

    # Basic configuration to get Active Directory working
    # Please dont forget about Security Groups - AWS or any netowrk firewalls , VPCs, Subnets, Etc. 
    $ sudo ufw allow ssh
    $ sudo ufw enable
    $ sudo ufw status numbered
    $ sudo ufw allow 8443/tcp
    $ sudo ufw allow 88/tcp
    $ sudo ufw allow 135/tcp
    $ sudo ufw allow 139/tcp
    $ sudo ufw allow 445/tcp
    $ sudo ufw allow 464/tcp
    $ sudo ufw allow 389/tcp 
    # If you install additonal modules, need to allow them as well.
    # If you install the firewall , it disables ufw and allows all traffic. 

How to Add Linux 
---------------

    # There is a bug here opened up a github issue
    # https://github.com/zentyal/zentyal/issues/2115
    # How to find your AD name
    # Login > Domain > Realm > ad01.decyphertek
    # Set the Administrator Password
    # Login > Users & Computers > Manage > Users > Adminotrator > Set password.
    # Server side, find the private IP
    $ ifconfig
    # On the client side , set hosts to reference AD IP - EXAMPLE
    $ sudo vim /etc/hosts
    172.31.27.20 ad01.decyphertek
    # Install required software to join to AD.
    $ sudo apt install -y sssd sssd-ad sssd-tools realmd libnss-sss libpam-sss adcli samba-common-bin 
    $ sudo realm -v discover ad01.decyphertek
    $ sudo join -v ad01.decyphertek
    $ sudo pam-auth-update --enable mkhomedir
    # Optional: If you want to utilize Kerberos Tickets.
    $ sudo apt install krb5-user smbclient cifs-utils winbind
    $ smbclient -L ad01.decyphertek

References
----------

    https://doc.zentyal.org/en/installation.html#installation-on-top-of-ubuntu-20-04-lts-server-or-desktop
    https://wiki.zentyal.org/wiki/Installation_Guide
    https://doc.zentyal.org/en/
    https://learn.microsoft.com/en-us/answers/questions/268557/active-directory-domain-controler-to-client-requir.html
    https://ubuntu.com/server/docs/service-sssd-ad
    https://www.server-world.info/en/note?os=Ubuntu_22.04&p=realmd
    https://ubuntu.com/server/docs/service-kerberos