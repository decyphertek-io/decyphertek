LXC - Linux Containers
=======================

"LXC is a userspace interface for the Linux kernel containment features. Through a powerful API and simple tools, it lets Linux users easily create and manage system or application containers."

Install LXC:
-----------
```
sudo apt install -y lxc
```

lxc Terminal Commands:
----------------------
* On debian 12 , it doesnt work with just an LXC install, troubleshooting. 
```
# create a new Debian container
sudo lxc-create -n decyphertek-debian -t debian -- -r bookworm
# start the Debian container
sudo lxc-start -n decyphertek-debian
# attach to the Debian container
sudo lxc-attach -n decyphertek-debian
# create a new Ubuntu container
sudo lxc-create -n decyphertek-ubuntu -t ubuntu
# start the Ubuntu container
sudo lxc-start -n decyphertek-ubuntu
# attach to the Ubuntu container
sudo lxc-attach -n decyphertek-ubuntu
# copy or clone containers
sudo lxc-copyF
# destroy a container
sudo lxc-destroy
# stop a running container
sudo lxc-stop
# freeze all the container's processes
sudo lxc-freeze
# unfreeze all the container's processes
sudo lxc-unfreeze
# display information about a container
sudo lxc-info
# list containers
sudo lxc-ls
# attach to the console of a container
sudo lxc-console
# monitor container events
sudo lxc-monitor
# wait for a specific container state
sudo lxc-wait
# get or set the cgroup attributes of a container
sudo lxc-cgroup
# autostart containers
sudo lxc-autostart
# check the current kernel for sudo lxc support
sudo lxc-checkconfig
# update container configuration to the latest version
sudo lxc-update-config
# snapshot a container
sudo lxc-snapshot
# restore a container snapshot
sudo lxc-restore
# query sudo lxc system configuration
sudo lxc-config
# execute a command in a temporary container
sudo lxc-execute
# run a command inside an existing container
sudo lxc-attach
# execute a process with a new user namespace
sudo lxc-usernsexec
# query or set configuration values for the container or the host
sudo lxc-config
```

References:
-----------

https://linuxcontainers.org/lxc/introduction/
