Jupyterhub
=====

Jupyterhub is an open source Data Science multi-user notebook that supports Python, R , and even GNU Octave.  

Install
-------

     $ sudo apt update 
     $ sudo su -c "curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -"
     $ curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - 
     $ sudo apt-get install -y nodejs 
     $ sudo npm install -g configurable-http-proxy
     $ sudo apt install -y python3-pip  
     $ sudo -H python3 -m pip install importlib-metadata zipp -U
     $ sudo -H python3 -m pip install jupyterhub jupyterlab notebook PyJWT oauthenticator 
     $ sudo mkdir /etc/jupyterhub/
     $ cd /etc/jupyterhub/
     $ sudo jupyterhub --generate-config
     $ sudo su -c "curl 'https://raw.githubusercontent.com/decyphertek-io/configs/main/jupyterhub_config.py' >> /etc/jupyterhub/jupyterhub_config.py"
     $ sudo chmod 700 /etc/ssl/private
     $ sudo openssl req -x509 -nodes -days 1095 -newkey rsa:2048 -keyout /etc/ssl/private/private-ssl.key -out /etc/ssl/certs/private-ssl.crt -subj "/C=US/ST=Any/L=Anytown/O=decyphertek-io/OU=adminotaur/CN=decyphertek"

New User/Hostname
-----------------

     # The -m option after useradd, will make a home directory.
     $ sudo useradd -m username
     $ sudo passwd username
     # Optional: Add to sudo group
     $ sudo usermod -aG sudo username
     # Optional: No sudo password for username, add the following line under %sudo. 
     $ sudo visudo
     username ALL=(ALL) NOPASSWD:ALL
     # Optional: Fix bash shell not showing username and hostname
     $ sudo chsh -s /bin/bash username
     # Optional: Change hostname - Logout/login to see changes.
     $ sudo hostnamectl set-hostname "hostname-here"
     $ sudo su -c "echo '127.0.1.1 hostname-here' >> /etc/hosts"
  
Systemd Managed Jupyterhub
--------------------------

     $ sudo su -c "curl 'https://raw.githubusercontent.com/decyphertek-io/configs/main/jupyterhub.service' >> /etc/systemd/system/jupyterhub.service"
  
Config - Azure MFA Setup
------------------------

     # Azure AD > Tenant Properties > Tenant ID 
     # Azure AD > Enterprise Apps > Create new App > APP ID 
     # Azure AD > App Registration > Certs & Secrets > Create a new secret ID
     # Azure AD > AppRegistration > Authetntication > Add https://ip-or-domain/hub/oauth_callback

     $ sudo vim /etc/jupyterhub/jupyterhub_config.py   
     ###Azure AD MFA ### 
     from oauthenticator.azuread import AzureAdOAuthenticator 
     c.JupyterHub.authenticator_class = AzureAdOAuthenticator 
     c.Application.log_level = 'DEBUG' 
     c.AzureAdOAuthenticator.tenant_id = 'AAD_TENANT_ID'
     c.AzureAdOAuthenticator.oauth_callback_url = 'https://domain_or_ip/hub/oauth_callback' 
     c.AzureAdOAuthenticator.client_id = 'AAD_APP_CLIENT_ID'
     c.AzureAdOAuthenticator.client_secret = 'AAD_APP_CLIENT_SECRET'
     c.AzureAdOAuthenticator.scope = ['openid','profile']
     c.AzureAdOAuthenticator.username_claim = ‘upn' OR 'given_name’

     ###Server Config### 
     #0.0.0.0 if using PAM, if using AzureAD , need to set server IP. Can set any port, avoid port conflicts.
     c.JupyterHub.ssl_key = '/etc/ssl/private/private-ssl.key' 
     c.JupyterHub.ssl_cert = '/etc/ssl/certs/private-ssl.crt'
     c.JupyterHub.ip = '0.0.0.0' 
     c.JupyterHub.port = 443

     ###Admin Spawner### 
     c.JupyterHub.admin_access = True 

     ###Notebook Idle Shutdown### 
     c.ServerApp.shutdown_no_activity_timeout = 60 * 60
     c.MappingKernelManager.cull_idle_timeout = 20 * 60
     c.MappingKernelManager.cull_interval = 2 * 60

     ###Custom Logo###
     c.JupyterHub.logo_file = '/usr/local/share/jupyterhub/static/images/logo.png'

     ###Allowed Multiple named Servers###
     c.JupyterHub.allow_named_servers = True
     c.JupyterHub.named_server_limit_per_user = 5

     #Any port can be set, avoid port conflicts
     #AWS Security group - allow tcp inbound on port 

SSSD Install
-------------

     $ sudo apt install sssd sssd-tools libnss-sss libpam-sss samba-common-bin packagekit python3-sss realmd
     $ sudo su -c "curl 'https://raw.githubusercontent.com/decyphertek-io/configs/main/sssd.conf' >> /etc/sssd/sssd.conf"
     # Use realmd to add to AD, if issues with sssd on certain OS versions. 
     $ sudo systemctl restart sssd 
     # SSH into server - yourusername@ip-of-server

Optional:How to setup and install R on JupyterHub
----------------------------------------
    
     !!! Caution - This is Experimental and may not work correctly !!!
     $ sudo apt install r-base
     $ jupyter kernelspec list
     $ sudo mkdir /usr/local/share/jupyter/kernels/R/
     $ sudo su -c "curl 'https://raw.githubusercontent.com/decyphertek-io/configs/main/kernel.json' >> /usr/local/share/jupyter/kernels/R/kernel.json"
     # Login as your user in Jupyterhub and openup a terminal
     $ which R
     $ /usr/bin/R
     > install.packages('IRkernel')
     # Yes to all ( Have to select your own user env choice ) 
     # Log out and back in . 
 
Managing Server
---------------

     # Start the server
     $ sudo systemctl start jupyterhub
     # Stop the server
     $ sudo systemctl stop jupyterhub
     # restart server
     $ sudo systemctl restart jupyterhub
     # check status
     $ sudo systemctl status jupyterhub
     # enable on startup
     $ sudo systemctl enable jupyterhub

TroubleShooting
---------------

     $ sudo jupyterhub -f /etc/jupyterhub/jupyterhub_config.py | logger -t jupyterhub
     $ sudo jupyter troubleshooting --help
     $ sudo jupyterhub --debug
     $ ps aux | grep jupyterhub
     $ sudo kill -9 pid

Upgrade
-------

     $ sudo -H python3 -m pip install --upgrade jupyterhub== <version> 
     $ sudo jupyterhub upgrade-db
     
Optional: Python3 packages
--------------------------

     $ sudo -H python3 -m pip install numpy scipy matplotlib pandas

Optional: CIS Can break permisisons
------------------------------------

     $ sudo chmod 644 /usr/share/keyrings/nodesource.gpg
     

References
-----------

     https://jupyterhub.readthedocs.io/en/stable/quickstart.html#prerequisites
     https://jupyterhub.readthedocs.io/en/stable/getting-started/authenticators-users-basics.html
     https://jupyterhub.readthedocs.io/en/stable/troubleshooting.html
     https://aws.amazon.com/premiumsupport/knowledge-center/ec2-static-dns-ubuntu-debian
     https://hpc.llnl.gov/services/jupyterhub-and-jupyter-notebooks/jupyterhub-r-kernel
     https://github.com/nodesource/distributions/issues/1181

