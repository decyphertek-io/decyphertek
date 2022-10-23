Caldera
=====

A Scalable, Automated Adversary Emulation Platform

Install
--------

     $ sudo apt update && sudo apt upgrade -y
     $ sudo apt install git python3-pip
     $ git clone https://github.com/mitre/caldera.git --recursive 
     $ cd caldera 
     $ sudo -H python3 -m pip install -r requirements.txt

Systemd Managed Caldera
-----------------------

     $ sudo vim /etc/systemd/system/caldera.service
     [Unit]
     Description=caldera
     After=syslog.target network.target
     [Service]
     User=root
     WorkingDirectory=/home/$USER/caldera/
     ExecStart=/usr/bin/python3 /home/$USER/caldera/server.py 
     [Install]
     WantedBy=multi-user.target
     $ sudo systemctl daemon-reload

Mange Caldera
-------------

     $ sudo systemctl enable caldera
     $ sudo systemctl start caldera
     $ sudo systemctl status caldera

Login
-----

     # http://ip-of-server:8888 
     # user = admin
     # password = admin
     # If you have a firewall or Security group , allow port 8888
     # Example:
     $ sudo ufw allow 8888/tcp


Setup SSL Cert
--------------
    
     # Mod default settings 
     $ sudo apt install haproxy
     $ sudo systemctl enable haproxy
     $ sudo systemctl restart haproxy
     $ vim /home/$USER/caldera/conf/default.yml
     <AND>
     $ vim /home/$USER/caldera/conf/local.yml
     app.contact.http = https://0.0.0.0:8443
     $ vim /home/$USER/caldera/conf/default.yml
     # Enable the SSL Plugin on the default.yml by adding it.
     $ vim /home/$USER/caldera/conf/default.yml
     plugins:
     - ssl
     # Consider replacing - /home/$USER/caldera/plugins/ssl/conf/insecure_certificate.pem
     $ sudo systemctl daemon-reload
     $ sudo systemctl restart caldera
     # https://ip-of-server:8443

Update Passwords
----------------

     $ vim /home/$USER/caldera/conf/default.yml
     Example:


References
----------

     https://caldera.mitre.org/
     https://caldera.readthedocs.io/en/latest/Installing-CALDERA.html
     https://caldera.readthedocs.io/en/latest/Getting-started.html
     https://caldera.readthedocs.io/en/latest/Plugin-library.html
     