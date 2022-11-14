Ansible
=====

Ansible is an automation platform that can manage multiple technologies, 
including Linux, Windows, Mac, firewalls, routers, switches, and many more. 

Install
--------

     # Ubuntu Install
     $ sudo apt update
     $ sudo apt install software-properties-common
     $ sudo add-apt-repository --yes --update ppa:ansible/ansible
     $ sudo apt update
     $ sudo apt install ansible
  
     # Mac Install via Python
     $ curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
     $ python3 --version
     $ export PATH=$HOME/bin:~/Library/Python/<version>/bin:$PATH
     $ python3 get-pip.py --user
     $ python3 -m pip install --upgrade pip
     $ python3 -m pip install --user ansible
     $ python3 -m pip install --user paramiko
     # Upgrade
     $ python3 -m pip install --upgrade --user ansible

     # Fedora Install
     $ sudo dnf update
     $ sudo dnf install ansible
 
     # Config/Setup
     # Ubuntu
     $ sudo vim /etc/ansible/ansible.cfg
     # Mac 
     $ vim ~/.ansible.cfg

AWS Cli Install/Setup
---------------------

     # Ubuntu
     $ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
     $ unzip awscliv2.zip
     $ sudo ./aws/install
     $ sudo aws configure
     # This saves aws creds under root user.
     # Mac
     $ python3 -m pip install --user awscli

 
Collections - AWS Example
--------------------------

     # Ubuntu
     $ sudo ansible-galaxy collection install amazon.aws
     $ cd /etc/ansible/.ansible/collections/ansible_collections/amazon/aws
     # Install Python requirements
     $ sudo -H pip3 install -r requirements.txt
     # Mac
     $ ansible-galaxy collection install amazon.aws
     $ cd ~/.ansible/collections/ansible_collections/amazon/aws
     # Install Python requirements
     $ python3 -m pip install -r requirements.txt
  
Vault
------

     # Ubuntu uses sudo and located at /etc/ansible/
     # Mac doesnt use sudo and located at home directory ~ . 
     # Easy way , just encrypt the vars file
     $ ansible-vault encrypt variables.vault
     # Choose a password. 
     # Example of a variable.vault
     ip_address: 'iphere'
     api_key: 'apikeyhere'
     # Make sure Playbook references vars
     # Can reference in ansible.cfg if using just one vault.
     vars_files:
       - ~/ansible/vault/variables.vault
     # vars being referenced stored in ansible vault, example
     vars:
       - ip_address: '{{ ip_address }}'
       - api_key: '{{ api_key }}'
     # Need to edit the vault, no probs
     $ ansible-vault edit variables.vault
     # How to decrypt vault and use with a playbook.
     $ ansible-playbook -l firewall panos_facts.yml --ask-vault-pass

Decyphertek Ansible
--------------------

     # Ubuntu
     # mac no sudo and run from home directory
     $ cd /etc/ 
     $ sudo rm -rf ansible
     $ sudo git clone https://github.com/decyphertek-io/ansible.git
     $ cd ansible/config
     $ sudo cp ansible.cfg /etc/ansible/
     # Run git fetch to recieve the newest updates to the repo. 
     $ cd /etc/ansible
     $ git fetch

Version Control
----------------

     # Clone your branch of ansible
     # https://your-git
     # Ex: Your branch name will differ
     $ git clone https://your.git
     $ cd ansible
     # EX: Checkout you branch - Yours will be different
     $ git checkout ansible
     $ git status
     $ git add .
     $ git commit -m "Add a comment"
     $ git push
     # The git push command will create a pull request link, visit the link and create the pull request to be approved and merged.
     # Can also setup ssh git instead of using a password , see reference doc below.
     # Can push git changes in desktop gui via VsCodium
     $ sudo snap install codium
 
General guidance
----------------

     # AWS Cli Command via playbook
     $ AWS_PROFILE=us-east-1 ansible-playbook -l local aws-gather-info.yaml
     # Run a basic playbook command
     $ ansible-playbook -l test_server playbook.yaml
     # How to use Vault:( See Vault instructions for more details ) 
     $ ansible-playbook -l test_server playbook.yml --ask-vault-pass 
     # How to run Windows Playbooks
     $ ansible-playbook -l win template.yml --ask-vault-pass
     # Modify the ansible.cfg to point to your right directories
     $ vim ~/.ansible.cfg
     # Modify the hosts 
     $ vim ~/ansible/inventory/hosts
     # have to setup ~.aws/config & ~.aws/credentials
     $ aws configure
 
Docs
-----

     $ ansible-doc --version
     $ ansible-doc -h
     # Module info:
     $ ansible-doc <module name> >>> Example
     $ ansible-doc copy
     # Plugin info:
     $ ansible-doc --type <plugin type>  >>> Example
     $ ansible-doc -t connection -s ssh
 
 
References
----------

     https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
     https://docs.ansible.com/ansible/latest/cli/ansible-doc.html
     https://docs.ansible.com/ansible/latest/cli/ansible-vault.html
     https://support.atlassian.com/bitbucket-cloud/docs/set-up-an-ssh-key/
     https://docs.paloaltonetworks.com/pan-os/9-0/pan-os-panorama-api/get-started-with-the-pan-os-xml-api/get-your-api-key.html
