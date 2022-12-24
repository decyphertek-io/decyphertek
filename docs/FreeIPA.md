Free IPA
========

Open Source Active Directory Alternative. 

Install - Rocky Linux 8.6
--------------------------

    $ sudo hostname set-hostnamectl ad1.decyphertek.io
    $ sudo ip addr
    $ sudo vi /etc/hosts
    ip-of-server ad1.decyphertek.io
    $ sudo dnf module enable idm:DL1
    $ sudo dnf install ipa-server ipa-server-dns firewalld -y
    $ sudo systemctl unmask firewalld
    $ sudo systemctl start firewalld
    $ sudo systemctl enable firewalld
    $ sudo firewall-cmd --add-service={http,https,dns,ntp,freeipa-ldap,freeipa-ldaps} --permanent
    $ sudo firewall-cmd --reload
    $ sudo firewall-cmd --list-all
    # Confirm you see inet6
    $ sudo ip a
    # Enter hostname created above was an example. 
    # Warning - single label domains are not supported
    $ sudo ipa-server-install --setup-dns --allow-zone-overlap

    The IPA Master Server will be configured with:
    Hostname:       ad1.decyphertek.io
    IP address(es): 172.31.23.159
    Domain name:    decyphertek.io
    Realm name:     DECYPHERTEK.IO

    The CA will be configured with:
    Subject DN:   CN=Certificate Authority,O=DECYPHERTEK.IO
    Subject base: O=DECYPHERTEK.IO
    Chaining:     self-signed

    BIND DNS server will be configured to serve IPA domain with:
    Forwarders:       172.31.0.2
    Forward policy:   only
    Reverse zone(s):  No reverse zone

    Continue to configure the system with these values? [no]: yes

    $ kinit admin
    $ klist
    # Need to make sure your system can point to the domain.
    # Ip redirects to domain, I use linux , so added it to my /etc/hosts 
    # This may differ in Windows or Mac . 
    # Client side
    $ sudo vim /etc/hosts
    ip-of-server ad1.decyphertek.io
    # https://ip-or-domain/ipa/ui/

Ports & Protocols
----------------

    TCP Ports:
    * 80, 443: HTTP/HTTPS
    * 389, 636: LDAP/LDAPS
    * 88, 464: kerberos
    * 53: bind
    UDP Ports:
    * 88, 464: kerberos
    * 53: bind
    * 123: ntp

References
----------

    https://www.freeipa.org/page/Main_Page
    https://www.freeipa.org/page/Quick_Start_Guide
    https://www.howtoforge.com/how-to-install-freeipa-on-rocky-linux