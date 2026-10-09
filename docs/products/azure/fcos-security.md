FCOS Basics
-----------

Decyphertek has secured your Azure VM with one or more of the following open source software. Please reference the specific software stack your server has. [Azure Marketplace: Decyphertek ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=decyphertek.io&page=1)

Note:
------
Please be aware that it takes a few minutes for the system to be up and running. The best way to check is to view the VM status from the Azure console > Virtual Machines. If it says Running, the VM is ready.
* Make sure you allow ssh via network security group.

SSH Into the server:
---------------------
* Utilize Azure SSH settings to set your ssh keys AND/OR Password to ssh in.
* Linux + MAC - add .pem key to ~/.ssh/id_rsa > change permissions > chmod 400 id_rsa
* ssh core@ip-of-server ( user set during deployment, default: core )
* If using putty or mobaxterm make sure to convert .pem using puttygen.

Passwords - DB AND/OR User:
---------------------------
* ssh into server
* Some allow creating user/pass on first login
* If no then you can find your passwords here:
* cat ~/.podman/.env
* This will display the randomly generated passwords for DB AND/OR User.

Server Purchased:
----------------
* Please reference your instructions on the Azure Marketplace for your purchased server.

Podman - Update Containers:
---------------------------
* Caution: Make sure to back up any data and test the update in a staging environment before running these commands on a production server.
* ssh into the server
```
cd .podman
podman-compose down
podman-compose pull
podman-compose up -d
```

Manage Fedora CoreOS ( FCOS ):
----------------------
* Optional: Manually update FCOS. Updates will happen automatically.
* To manually check and apply updates, ssh into the server and run:
```
sudo rpm-ostree upgrade
rpm-ostree status
```

References:
-------------

    https://docs.podman.io/
    https://github.com/containers/podman-compose
    https://docs.fedoraproject.org/en-US/fedora-coreos/
