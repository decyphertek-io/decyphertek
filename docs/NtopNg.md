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
    # Change config - Not much here.
    $ sudo ntopng-config
    # Set to Https 
    $ sudo systemctl stop ntopng
    # This is temporary test and isnt controlled by systemd
    $ sudo ntopng --https=443 & 
    # Edit the configuration so that systemd controls config. Unlcear what to change?
    $ sudo vim /etc/ntopng/ntopng.conf
    # Solution is to create your own systemd service
    $ sudo vim /etc/systemd/system/ntopng-mod.service
    [Unit]
    Description=ntopng-mod
    After=syslog.target network.target
    [Service]
    User=root
    ExecStart=/usr/bin/ntopng --https=443
    [Install]
    WantedBy=multi-user.target
    $ sudo systemctl stop ntopng
    $ sudo sysemctl start ntopng-mod

    
References
-----------

    https://www.ntop.org/products/traffic-analysis/ntop/#ntopng-screenshots
    https://github.com/ntop/ntopng
    https://packages.ntop.org/
    https://packages.ntop.org/apt-stable/
    https://github.com/ntop/ntopng/blob/dev/doc/README.md
    https://www.ntop.org/guides/ntopng/faq.html#cannot-login-into-the-gui
    https://www.ntop.org/ntopng/best-practices-to-secure-ntopng/