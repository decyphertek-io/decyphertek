Incus - Linux Containers
=========================

Incus is a fork of Canonical's LXD . 

Incus install:
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

Incus basics:
-------------

    $ sudo adduser $USER incus-admin
    $ newgrp incus-admin
    $ incus admin init --minimal
    $ incus image list images:
    $ incus launch images:ubuntu/22.04 NAMEHERE
    $ incus list
    $ incus start NAMEHERE
    $ incus info NAMEHERE
    $ incus copy NAMHERE COPYOFNAMEHERE
    $ incus stop NAMHERE


References:
------------

https://github.com/zabbly/incus
https://linuxcontainers.org/incus/docs/main/
