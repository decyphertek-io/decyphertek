Semaphore UI is an open-source platform designed to manage Ansible, OpenTofu, Terraform and bash scripts via a web browser. 
It provides a user-friendly interface for orchestrating and automating infrastructure tasks, making it easier for 
developers and teams to streamline workflows and reduce manual errors. With its integration capabilities and scalable 
design, Semaphore UI offers a centralized and efficient solution for infrastructure management. [GCP Marketplace: Semaphore UI ](https://console.cloud.google.com/marketplace/product/server-build-415714/semaphore-ui-ansible-opentofu)

Note:
------
* Please be aware that it takes a few minutes for Semaphore to be up and running.

SSH Into the server:
--------------------
* Utilize Google SSH Console or setup ssh keys or password.

Semaphore login & password:
------------------------------
* Run from Terminal to find your password:
```
sudo cat /home/semaphore/passwords.txt
```
* Go to your browser:
```
https://ip-of-server
```
* Login to Semaphore UI: 
```
username: semaphore 
password: (SEMAPHORE_USER_PASS listed in passwords.txt)
```
* Optional: Change Semaphore Password - Bottom left > Click on semaphore > Edit Accounts > Enter your new password . 
* Login to mariadb from terminal : 
```
sudo mysql -u root -p  
Password: (SEMAPHORE_DB_PASS listed in passwords.txt)
```
* Ansible playooks/roles : 
```
sudo su semaphore
cd /home/semaphore/.ansible/
ls 
cd playbooks
# OR
cd roles
```

Setup Ansible in Semaphore: 
---------------------------
* Create a project: Can be accessed on the main page when you first log in.
* Create an Environment {}: On the left side, select Environment > Select New Environment (can be empty {} or have env variables).
* Add an ssh key/Password to keystore: On the left side, select Key Store > Select New Key > enter name key & select ssh key or password.
* Create an Inventory: On the left side, select Inventory > Enter name, select saved credentials, select Static (Hosts).

```
[test_server]
172.31.95.4 ansible_host=172.31.95.4 ansible_user=admin
```

* Create a repository : Left side, Select Repositories > Select New Repository:
```
Name: Ansible
URL or Path: /home/semaphore/.ansible/playbooks/ 
Key: ( Select your SSH Key )
* Create a Task Template : Semaphore UI > Task Template > New Template > Select Ansible: ( EX:)

```
Name: UFW Install
Playbook Filename: /home/semaphore/.ansible/playbooks/ufw/ufw_install.yml
Select established : Inventory , Repository , Environment . 
```

* Before you run a task playbook, you need to ssh into the target server from semaphore via terminal. 
* Login terminal > add your private key > ssh into target server, so it gets added to known_hosts.

```
sudo su semaphore
cd ~
vim ~/.ssh/id_rsa 
chmod 400 id_rsa 
ssh username@ip-of-server
```

* Run a Task/playbook : Left side Task Templates > Select RUN next to the task.

Setup Opentofu in Semaphore:
----------------------------
* From terminal run , to setup gcloud:
```
sudo su semaphore
cd ~
gcloud init
```
* Login via provided URL Link in terminal. It will generate an auth code, Copy and enter that auth code into the terminal.
# To reauthenticate in the future , run:
```
gcloud auth login --no-launch-browser
```
* To find some information useful for terraform / Opentofu:
```
gcloud projects list
gcloud compute zones list
```
* I provided an example to get started and terraform-docs-samples:
```
sudo su semaphore
cd ~
cd .opentofu/gcp/
ls
cd compute
# OR
cd terraform-dodcs-samples
```
* Setup Opentofu repo: Semaphore UI > Repositories > New Repository :
```
Name: Opentofu
URL or Path: /home/semaphore/.opentofu/
Access Key: NONE
```
* Create a Task Template : Semaphore UI > Task Template > New Template > Select OpenTofu Code: ( EX:)
'''
Name: GCP Create VM
Subdirectory Path: gcp/compute-dev/create_vm/
Repository: Opentofu
Environment: Empty
```
* Run Task Template . 


Troubleshooting:
-----------------
* Make sure you are accessing https://ip-of-server
* Your passwords are in /home/semaphore/passwords.txt :
```
sudo cat /home/semaphore/passwords.txt
```
* Make sure you setup , projects , Environment , ssh key , inventory , repository , and task . 
* Ensure public ssh key is on the target server & there is a route, so Ansible Sempahore can run properly.
* Manage semaphore from systemd: 
```
sudo systemctl status semaphore
```
* Manage nginx from systemd: 
```
sudo systemctl status nginx
```

Additonal Security Features:
----------------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and at 3am daily.

References:
------------
* https://www.semui.co/
* https://docs.semui.co/
* https://docs.ansible.com/
* https://opentofu.org/docs/
* https://cloud.google.com/docs/terraform/samples
* https://github.com/terraform-google-modules/terraform-docs-samples

