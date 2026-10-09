Flatcar Basics
--------------

Decyphertek has secured your GCP VM with one or more of the following open source software. Please reference the specific software stack your server has. [GCP Marketplace: Decyphertek ](https://console.cloud.google.com/marketplace/browse?filter=partner:decyphertek.io)

Note:
------
Please be aware that it takes a few minutes for the system to be up and running. The best way to check is to view the VM status from the GCP console > Compute Engine > VM Instances. If it shows a green check mark, the VM is ready.

SSH Into the server:
---------------------
* Utilize GCP to setup your user and ssh keys.
    * GCP Console > Compute Engine > VM Instances > Click SSH button > View gcloud command
* Linux + MAC - add .pem key to ~/.ssh/id_rsa > change permissions > chmod 400 id_rsa
* ssh core@ip-of-server ( reference your VMs external ip )
* If using putty or mobaxterm make sure to convert .pem using puttygen.
* Networking: Make sure you allow ssh via the firewall rules , ufw allows ssh , and you have public or private vpn access.

Passwords - DB AND/OR User:
---------------------------
* ssh into server
* Some allow creating user/pass on first login
* If no then you can find your passwords here:
* cat ~/.docker/.env
* This will display the randomly generated passwords for DB AND/OR User.

Server Purchased:
----------------
* Please reference your instructions on the GCP Marketplace for your purchased server.

Portainer - Manage Docker:
---------------------------
* How to access Portainer to manage your containers > https://ip-of-server:9443
* Follow the instructions to create a new admin account.
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then run > docker restart portainer
* Once logged into portainer, click get started and select local. You can manage docker from here.

Docker - Update Containers:
---------------------------
* Caution: Make sure to back up any data and test the update in a staging environment before running these commands on a production server.
* ssh into the server
```
cd .docker
docker-compose down
docker-compose pull
docker-compose up -d
```

Manage Flatcar Linux:
----------------------
* Optional: Manually update Flatcar. Updates will happen automatically.
* Flatcar is immutable , the OS is read-only , all apps run via docker.
* If you want to manually check for updates run this command: update_engine_client -update

References:
-------------

    https://www.flatcar.org/docs/latest
    https://docs.docker.com/
    https://docs.portainer.io/
