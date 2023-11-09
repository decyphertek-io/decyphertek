LXC - Linux Containers
=======================

"LXC is a userspace interface for the Linux kernel containment features. Through a powerful API and simple tools, it lets Linux users easily create and manage system or application containers."

Install LXC:
-----------

    $ sudo apt install lxc

Install LXC Web Panel:
-----------------------

    #Debian Install script
    wget https://lxc-webpanel.github.io/tools/install.sh -O - | bash
    #Auto Update Script
    wget https://lxc-webpanel.github.io/tools/update.sh -O - | bash
    Connect you on http://your_ip_address:5000/
    Login with user admin and password admin

LXC Terminal Commands:
----------------------

    * create a new Debian container
    $ lxc-create -n decyphertek-debian -t debian

    * start the Debian container
    $ lxc-start -n decyphertek-debian

    * attach to the Debian container
    $ lxc-attach -n decyphertek-debian

    * create a new Ubuntu container
    $ lxc-create -n decyphertek-ubuntu -t ubuntu

    * start the Ubuntu container
    $ lxc-start -n decyphertek-ubuntu

    * attach to the Ubuntu container
    $ lxc-attach -n decyphertek-ubuntu

    * copy or clone containers
    $ lxc-copy

    * destroy a container
    $ lxc-destroy

    * stop a running container
    $ lxc-stop

    * freeze all the container's processes
    $ lxc-freeze

    * unfreeze all the container's processes
    $ lxc-unfreeze

    * display information about a container
    $ lxc-info

    * list containers
    $ lxc-ls

    * attach to the console of a container
    $ lxc-console

    * monitor container events
    $ lxc-monitor

    * wait for a specific container state
    $ lxc-wait

    * get or set the cgroup attributes of a container
    $ lxc-cgroup

    * autostart containers
    $ lxc-autostart

    * check the current kernel for LXC support
    $ lxc-checkconfig

    * update container configuration to the latest version
    $ lxc-update-config

    * snapshot a container
    $ lxc-snapshot

    * restore a container snapshot
    $ lxc-restore

    * query LXC system configuration
    $ lxc-config

    * execute a command in a temporary container
    $ lxc-execute

    * run a command inside an existing container
    $ lxc-attach

    * execute a process with a new user namespace
    $ lxc-usernsexec

    * query or set configuration values for the container or the host
    $ lxc-config

References:
-----------

https://linuxcontainers.org/lxc/introduction/
https://lxc-webpanel.github.io/install.html