NtopNG
=====

Ntopng is the next generation version of the original ntop, a network traffic 
probe that monitors network usage.

Install
-------

    $ sudo apt-get install software-properties-common wget 
    $ sudo add-apt-repository universe 
    $ wget https://packages.ntop.org/apt-stable/22.04/all/apt-ntop-stable.deb 
    $ sudo dpkg -i apt-ntop-stable.deb 
    $ sudo apt update 
    $ sudo apt install -y pfring-dkms nprobe ntopng n2disk cento
    # Manage NtopNG
    $ sudo systemctl [start|stop|restart|status|enable|disable] ntopng
    # Config
    $ sudo ntopng-config
    $ sudo vim /etc/ntopng/ntopng.conf
    # Login: Setup Account - https://localhost:3000
    # Optional: Sertup Nginx Reverse Proxy to rout traffic to port 443. See Decyphertek nginx docs. 
    
References
-----------

    https://www.ntop.org/products/traffic-analysis/ntop/#ntopng-screenshots
    https://github.com/ntop/ntopng
    https://packages.ntop.org/
    https://packages.ntop.org/apt-stable/
    https://github.com/ntop/ntopng/blob/dev/doc/README.md
    https://www.ntop.org/guides/ntopng/faq.html#cannot-login-into-the-gui
    https://www.ntop.org/ntopng/best-practices-to-secure-ntopng/