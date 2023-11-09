Inucs - Linux Containers
=========================

Incus is a fork of Canonical's LXD . 

Incus install
--------------

    $ curl -fsSL https://pkgs.zabbly.com/key.asc | gpg --show-keys --fingerprint
    $ mkdir -p /etc/apt/keyrings/
    $ sudo curl -fsSL https://pkgs.zabbly.com/key.asc -o /etc/apt/keyrings/zabbly.asc
    $ sudo vim /etc/apt/sources.list.d/zabbly-incus-stable.sources

    Enabled: yes
    Types: deb
    URIs: https://pkgs.zabbly.com/incus/stable
    Suites: bookworm
    Components: main
    Architectures: amd64
    Signed-By: /etc/apt/keyrings/zabbly.asc

    $ sudo apt update && sudo apt install incus

References:
------------

https://github.com/zabbly/incus
https://linuxcontainers.org/incus/docs/main/
