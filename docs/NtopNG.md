NtopNG
=====

"ntopng is the next generation version of the original ntop, a network traffic 
probe that monitors network usage."

Install
    $ sudo  apt install -y software-properties-common wget 
    $ sudo add-apt-repository universe 
    $ wget https://packages.ntop.org/apt-stable/20.04/all/apt-ntop-stable.deb 
    $ sudo dpkg -i apt-ntop-stable.deb 
    $ sudo apt update 
    $ sudo apt install -y pfring-dkms nprobe ntopng n2disk cento pfring-drivers-zc-dkms nedge 
    $ wget https://github.com/ntop/ntopng/blob/dev/doc/README.md
    

References
-----------

    https://www.ntop.org/products/traffic-analysis/ntop/#ntopng-screenshots
    https://github.com/ntop/ntopng
    https://packages.ntop.org/
    https://packages.ntop.org/apt-stable/
    https://github.com/ntop/ntopng/blob/dev/doc/README.md
    https://www.ntop.org/guides/ntopng/faq.html#cannot-login-into-the-gui