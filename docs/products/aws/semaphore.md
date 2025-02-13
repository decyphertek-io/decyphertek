Semaphore UI is a modern automation platform with an intuitive GUI, supporting Ansible, Terraform, OpenTofu, Bash, Python, and PowerShell. It’s a robust alternative to Ansible Tower or AWX, offering features like secure vault storage, scheduled playbook execution, and centralized task management. Decyphertek provides pre-configured playbooks and templates to help you get started quickly. [AWS Marketplace: Semaphore UI ](https://aws.amazon.com/marketplace/pp/prodview-5noeat2jipwca?sr=0-1&ref_=beagle&applicationId=AWSMPContessa)

Note:
-----
Please be aware that it can take 5-10 minutes for the system to be accessible. 

SSH Into the server:
--------------------
* Linux + MAC - add .pem key to 
```
~/.ssh/id_rsa
# change permisisons
chmod 400 id_rsa
ssh semaphore@ip-of-server
```
* If using putty or mobaxterm make sure to convert .pem using puttygen.

Semaphore login & password:
------------------------------
* Run from Terminal to find your password - cat passwords.txt
* Go to your browser - https://ip-of-server
* Login to semaphore gui - username: semaphore password: SEMAPHORE_USER_PASS listed in passwords.txt
* Optional: Change Semaphore Password - Bottom left > Click on semaphore > Edit Accounts > Enter your new password . 
* Login to mariadb from terminal : sudo mysql -u root -p  - Password: SEMAPHORE_DB_PASS listed in passwords.txt
* Change mariadb password : Login to terminal > sudo mysqladmin -u root -p'your_password' password "new_password"
* Ansible playooks/roles : cd /home/semaphore/.ansible - you can list the files in this directory - ls 

Setup Ansible / OpenTofu in Semaphore: 
---------------------------
* Create a project: Can be accessed on the main page when you first log in.
* Create an Environment {}: On the left side, select Environment > Select New Environment (can be empty {} or have env variables).
* Add an ssh key/Password to keystore: On the left side, select Key Store > Select New Key > enter name key & select ssh key or password.
* Create an Inventory: On the left side, select Inventory > Enter name, select saved credentials, select Static (Hosts).

```
[test_server]
172.31.95.4 ansible_host=172.31.95.4 ansible_user=admin
```

* Create a repository : Left side, Select Repositories > Select New Repository > Enter name , URL or Path = /home/semaphore/.ansible/playbooks/ , select key . 
* Create a Task Template : Runs an Ansible playbook

```
Name: decyphertek
Playbook Filename: /home/semaphore/.ansible/playbooks/ufw/ufw_install.yml
Select established : Inventory , Repository , Environment . 
```

* Before you run a task playbook, you need to ssh into the target server from semaphore via terminal. 
* Login Semaphore terminal > add your private key > ssh into target server, so it gets added to known_hosts.

```
vim ~/.ssh/id_rsa 
chmod 400 id_rsa 
ssh username@ip-of-server
```

* Run a Task/playbook : Left side Task Templates > Select RUN next to the task.
* Follow similar steps for Terraform / OpenTofu - https://docs.semui.co/user-guide/task-templates/terraform
* Opentofu Docs - https://opentofu.org/docs/

Troubleshooting:
-----------------
* AWS Basics - https://decyphertek.readthedocs.io/en/latest/products/aws-basics/
* Make sure you are accessing https://ip-of-server
* Your passwords are in /home/semaphore/passwords.txt - cat /home/semaphore/passwords.txt
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
---------------------------
* Ossec Hids - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Rsyslog - https://www.rsyslog.com/doc/index.html
* Automated Updates - Update script upon first boot and at 3am daily.

References:
------------
* https://docs.semaphoreui.com/