Foreman
=====

Foreman is a lifecycle managment platform that can be used to automate managing physical or virtual servers. 

Install {Fedora 28+ / Rocky Linux 9}
-------------------------------

     $ sudo dnf clean all
     $ sudo dnf localinstall https://yum.theforeman.org/releases/3.3/el8/x86_64/foreman-release.rpm
     $ sudo dnf localinstall https://yum.theforeman.org/katello/4.5/katello/el8/x86_64/katello-repos-latest.rpm
     $ sudo dnf install centos-release-ansible-29
     $ sudo dnf localinstall https://yum.puppet.com/puppet7-release-el-8.noarch.rpm
     $ sudo dnf config-manager --set-enabled powertools
     $ sudo dnf module enable katello:el8 pulpcore:el8
     $ sudo dnf update
     $ sudo dnf install foreman-installer-katello
     $ sudo foreman-installer --scenario katello
     # See details from terminal output on where to login.

Ansible Plugin
--------------

     # Enable Ansible plugin  
     $ sudo foreman-installer --enable-foreman-plugin-remote-execution \  
     > --enable-foreman-proxy-plugin-remote-execution-ssh --enable-foreman-plugin-ansible \ 
     > --enable-foreman-proxy-plugin-ansible --foreman-plugin-version latest 
     # Add Ansible Callbacks to ansible.cfg 
     [defaults] 
     callback_whitelist = foreman 

     [callback_foreman] 
     url = 'https://ip-or-domain.com' 
     ssl_cert = /etc/foreman-proxy/ssl_cert.pem 
     ssl_key = /etc/foreman-proxy/ssl_key.pem 
     verify_certs = /etc/foreman-proxy/ssl_ca.pem 
     # Then intiate the callback 
     $ sudo ansible -m setup test_server 

     # For a Host Group:  
     In the Foreman web UI, navigate to Configure > Host Groups, and select the host group that you want to use.  
     Click the Parameters tab, and in the Host Group Parameters area, click Add Parameter.  
     In the Name field, add the Ansible variable name.  
     From the Type list, select the type of the variable for validation.  
     In the Value field, enter the value for the variable.  

     # For a Host:  
     In the Foreman web UI, navigate to Hosts > All Hosts, and on the host that you want to use, click the Edit button.  
     Click the Parameters tab, and in the Host Parameters area, click Add Parameter.  
     In the Name field, add the Ansible variable name.  
     From the Type list, select the type of the variable for validation.  
     In the Value field, enter the value for the variable.  


References
----------

     https://docs.theforeman.org/3.3/Quickstart_Guide/index-katello.html
     https://docs.theforeman.org/nightly/Configuring_Ansible/index-foreman-deb.html  
     https://www.theforeman.org/plugins/foreman_ansible/2.x/index.html 
     https://github.com/theforeman/foreman_ansible 
     https://theforeman.org/plugins/foreman_ansible/3.x/index.html 
