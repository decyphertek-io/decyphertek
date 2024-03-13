Ansible Semaphore is a modern way to run ansible with an easy to use GUI. Its a good alternative to Ansible Tower
or AWX. You can store your vault secrets and run playbooks on a schedule. Decyphertek has also setup ansible with 
some basic playbooks to help you get started. 

SSH into the Semaphore server:
------------------------------

* Linux + Mac - add .pem key to ~/.ssh/id_rsa > change permisisons > chmod 400 id_rsa
* If using putty or mobaxterm make sure to convert .pem to .ppk using puttygen.
* Linux + Mac - ssh semaphore@ip-of-server
* Windows - utilize putty or mobaxterm

Semaphore login & password:
------------------------------

* Run from Terminal to find your password - cat passwords.txt
* Go to your browser - https://ip-of-server
* Login to semaphore gui - username: semaphore password: SEMAPHORE_USER_PASS listed in passwords.txt
* Optional: Change Semaphore Password - Bottom left > Click on semaphore > Edit Accounts > Enter your new password . 
* Login to mariadb from terminal : sudo mysql -u root -p  - Password: SEMAPHORE_DB_PASS listed in passwords.txt
* Ansible playooks/roles : cd /home/semaphore/.ansible - you can list the files in this directory - ls 

Setup Ansible in Semaphore: 
---------------------------

* Create a project:  Can be accessed on the main page when you first login.
* Create an Environment {} : Left side , Select Environment > Select New Environment ( Can be empty {} or have env variables )
* Add an ssh key/ Password to keystore : Left side , Select Key Store > Select New Key > enter name key & select ssh key or password
* Create an Inventory : Left side , select Inventory > Enter name , select saved credentials, select Static ( Hosts ).

    Ex:
    [test_server]
    172.31.95.4 ansible_host=172.31.95.4 ansible_user=admin

* Create a repository : Left side, Select Repositories > Select New Repository > Enter name , URL or Path = /home/semaphore/.ansible/playbooks/ , select access key.
* Create a Task Template : Runs an Ansible playbook

    EX:
    Name: decyphertek
    Playbook Filename: /home/semaphore/.ansible/playbooks/ufw/ufw_install.yml
    Select established : Inventory , Repository , Environment . 

* Before you run a task playbook, you need to ssh into the target server from semaphore via terminal. 
* Login Semaphore terminal > add your private key > ssh into target server, so it gets added to known_hosts.

    vim ~/.ssh/id_rsa 
    chmod 400 id_rsa 
    ssh username@ip-of-server

* Run a Task/playbook : Left side Task Templates > Select RUN next to the task.


Troubleshooting:
-----------------

* AWS Basics - https://decyphertek.readthedocs.io/en/latest/products/aws-basics/
* Make sure you are accessing https://ip-of-server
* Your passwords are in /home/semaphore/passwords.txt - cat /home/semaphore/passwords.txt
* Make sure you setup , projects , Environment , ssh key , inventory , repository , and task . 
* Ensure public ssh key is on the target server & there is a route, so Ansible Sempahore can run properly.
* Manage semaphore from systemd - sudo systemctl status semaphore
* Manage nginx from systemd - sudo systemctl status nginx

Additonal Security Features:
----------------------------

* Ossec Hids - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and at 3am daily.

References:
------------

https://www.semui.co/
https://docs.semui.co/