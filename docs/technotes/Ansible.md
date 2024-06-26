Ansible
=====

Ansible is an automation platform that can manage multiple technologies, 
including Linux, Windows, Mac, firewalls, routers, switches, and many more. 

Install
--------

     # Ubuntu Install
     sudo add-apt-repository --yes --update ppa:ansible/ansible
     sudo apt install ansible
  
     # Mac Install via Python
     curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
     python3 --version
     export PATH=$HOME/bin:~/Library/Python/<version>/bin:$PATH
     python3 get-pip.py --user
     python3 -m pip install --upgrade pip
     python3 -m pip install --user ansible
     python3 -m pip install --user paramiko
     # Upgrade
     python3 -m pip install --upgrade --user ansible

     # Fedora Install
     sudo dnf update
     sudo dnf install ansible
 
     # Config/Setup
     # Ubuntu
     sudo vim /etc/ansible/ansible.cfg
     # Mac 
     vim ~/.ansible.cfg

AWS Cli Install/Setup
---------------------

     # Ubuntu
     curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
     unzip awscliv2.zip
     # This saves aws creds under root user.
     # Beneficial if you have ansible installed via Linux at /etc/ansible/ 
     sudo ./aws/install
     sudo aws configure
     # Mac
     python3 -m pip install --user awscli

Collections - AWS Example
--------------------------

     # Ubuntu
     sudo vim /etc/ansible/ansible.cfg
     collections_paths = /etc/ansible/.ansible/collections/ansible_collections/
     sudo ansible-galaxy collection install amazon.aws
     cd /etc/ansible/.ansible/collections/ansible_collections/amazon/aws
     # Install Python requirements
     sudo apt install python3-pip
     sudo -H pip3 install -r requirements.txt
     # Mac
     ansible-galaxy collection install amazon.aws
     cd ~/.ansible/collections/ansible_collections/amazon/aws
     # Install Python requirements
     python3 -m pip install -r requirements.txt

      # Supported parameters include:
      wait, validate_certs, tags (resource_tags), access_key (aws_access_key, aws_access_key_id, ec2_access_key), security_group, profile (aws_profile), endpoint_url (aws_endpoint_url, ec2_url, s3_url), instance_type, vpc_subnet_id (subnet_id), aws_config, placement_group, network, wait_timeout, image, image_id, name, instance_initiated_shutdown_behavior, launch_template, termination_protection, detailed_monitoring, purge_tags, aws_ca_bundle, debug_botocore_endpoint_logs, count, exact_count, ebs_optimized, session_token (access_token, aws_security_token, aws_session_token, security_token), availability_zone, secret_key (aws_secret_access_key, aws_secret_key, ec2_secret_key), cpu_credit_specification, state, hibernation_options, security_groups, aap_callback (tower_callback), user_data, key_name, region (aws_region, ec2_region), filters, cpu_options, instance_ids, iam_instance_profile (instance_role),

     # AWS CLI - May need to use sudo if installed Linux way.
     aws ec2 describe-instances --query 'Reservations[].Instances[].[State.Name, InstanceId, ImageId, InstanceType, PublicIpAddress, SubnetId, VpcId,Tags[?Key==`Name`]| [0].Value]' --output table
     aws ec2 start-instances --instance-ids i-0000000000000
     aws ec2 stop-instances --instance-ids i-0000000000000
     aws ec2 terminate-instances --instance-ids i-0000000000000
  
Vault
------

     # Ubuntu uses sudo and located at /etc/ansible/
     # Mac doesnt use sudo and located at home directory ~ . 
     # Easy way , just encrypt the vars file
     ansible-vault encrypt variables.vault
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
     ansible-vault edit variables.vault
     # How to decrypt vault and use with a playbook.
     ansible-playbook -l firewall panos_facts.yml --ask-vault-pass

Decyphertek Ansible
--------------------

     # Ubuntu
     # mac no sudo and run from home directory
     cd /etc/ 
     sudo rm -rf ansible
     sudo git clone https://github.com/decyphertek-io/ansible.git
     cd ansible/config
     sudo cp ansible.cfg /etc/ansible/
     # Run git fetch to recieve the newest updates to the repo. 
     cd /etc/ansible
     sudo git fetch

Version Control
----------------

     # Clone your branch of ansible
     # https://your-git
     # Ex: Your branch name will differ
     git clone https://your.git
     cd ansible
     # EX: Checkout you branch - Yours will be different
     git checkout ansible
     git status
     git add .
     git commit -m "Add a comment"
     git push
     # The git push command will create a pull request link, visit the link and create the pull request to be approved and merged.
     # Can also setup ssh git instead of using a password , see reference doc below.
     # Can push git changes in desktop gui via VsCodium
     sudo snap install codium
 
General guidance
----------------

     # AWS Cli Command via playbook
     # Aws uses the default profile, add AWS_PROFILE=profilename before ansible-playbook command to use another.  
     sudo ansible-playbook aws-gather-info.yaml
     # AWS Module Playbook
     sudo ansible-playbook aws-ec2-launch.yml
     # Run a basic playbook command
     sudo ansible-playbook -l test_server playbook.yaml
     # How to use Vault:( See Vault instructions for more details ) 
     sudo ansible-playbook -l test_server playbook.yml --ask-vault-pass 
     # How to run Windows Playbooks
     sudo ansible-playbook -l windows template.yml --ask-vault-pass
     # Modify the ansible.cfg to point to your right directories
     sudo vim ~/.ansible.cfg
     # Modify the hosts 
     sudo vim ~/ansible/inventory/hosts
     # have to setup ~.aws/config & ~.aws/credentials
     sudo aws configure
 
Docs
-----

     ansible-doc --version
     ansible-doc -h
     # Module info:
     ansible-doc <module name> >>> Example
     ansible-doc copy
     # Plugin info:
     ansible-doc --type <plugin type>  >>> Example
     ansible-doc -t connection -s ssh
 
 
References
----------

     https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
     https://docs.ansible.com/ansible/latest/cli/ansible-doc.html
     https://docs.ansible.com/ansible/latest/cli/ansible-vault.html
     https://support.atlassian.com/bitbucket-cloud/docs/set-up-an-ssh-key/
     https://docs.ansible.com/ansible/latest/collections/amazon/aws/
     https://docs.ansible.com/ansible/latest/collections/amazon/aws/docsite/guide_aws.html#ansible-collections-amazon-aws-docsite-aws-intro
     https://docs.paloaltonetworks.com/pan-os/9-0/pan-os-panorama-api/get-started-with-the-pan-os-xml-api/get-your-api-key.html
