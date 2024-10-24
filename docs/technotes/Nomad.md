Nomad
======

"Manage containers, binaries, and VMs efficiently in the cloud, on-premises, and across edge environments."


Linux Install
-------------
```
sudo apt-get update && sudo apt-get install wget gpg coreutils
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt-get update && sudo apt-get install nomad
nomad -v
# If a manual install was chosen, make sure to add to path as discuessed in the reference. 
```

References
----------
```
* https://developer.hashicorp.com/nomad/tutorials/get-started/gs-install
* https://www.hashicorp.com/resources/nomad-flatcar-harmonious-marriage-of-lightweights
```
