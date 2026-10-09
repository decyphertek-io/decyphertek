Decyphertek has secured your AWS AMI with one or more of the following open source software. Please reference the specific software stack your server has. As a courteousy to AWS Subscribers this section can be used as a quick reference. [AWS Marketplace: Decyphertek ](https://aws.amazon.com/marketplace/seller-profile?id=851968a2-7d3c-4a0b-8c33-5351d91aaef1)

Note:
------
Please be aware that it takes a few minutes for the system to be up and running. The best way to check is to 
view the status check from the ec2 / instances / dashboard. If it says intializing, it is not ready yet. 

SSH Into the server:
---------------------
* Linux + MAC - add .pem key to ~/.ssh/id_rsa > change permisisons > chmod 400 id_rsa
* ssh core@ip-of-server 
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
* Please reference your instructions on AWS Marketplace for your purchased server.

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
* To manually check and apply updates run this command: 
```
sudo rpm-ostree upgrade --bypass-driver
```

Troubleshooting:
----------------
```
# SELinux troubleshooting
sudo sealert -a /var/log/audit/audit.log
sudo ausearch -m AVC,USER_AVC,SELINUX_ERR -ts boot -i

# Custom policy, then back to enforcing , only if issues found
sudo ausearch -m avc -ts recent | sudo audit2allow -M podman_policy
sudo semodule -i podman_policy.pp

# To disable SE Linux ( permissive - FCOS does not support fully disabled )
sudo sed -i 's/^SELINUX=.*/SELINUX=permissive/' /etc/selinux/config
sudo setenforce 0
sudo getenforce

# To re-enable SE Linux
sudo sed -i 's/^SELINUX=.*/SELINUX=enforcing/' /etc/selinux/config
sudo setenforce 1
sudo getenforce

sudo rpm-ostree status
```

References:
-------------
```
https://docs.podman.io/
https://github.com/containers/podman-compose
https://docs.fedoraproject.org/en-US/fedora-coreos/
```