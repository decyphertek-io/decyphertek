Caldera
=====

A Scalable, Automated Adversary Emulation Platform

Install
--------

     $ sudo apt update && sudo apt upgrade -y
     $ sudo apt install git python3-pip
     $ wget https://go.dev/dl/go1.19.2.linux-amd64.tar.gz
     $ sudo rm -rf /usr/local/go
     $ sudo tar -C /usr/local -xzf go1.19.2.linux-amd64.tar.gz
     $ export PATH=$PATH:/usr/local/go/bin
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
     ExecStart=/usr/bin/python3 /home/$USER/caldera/server.py --insecure
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
     $ python3 --verison 
     $ go version
     $ vim /home/$USER/caldera/conf/default.yml
     <AND>
     $ vim /home/$USER/caldera/conf/local.yml
     # Update both configs with the following info:
     app.contact.http = https://0.0.0.0:8443
     # Enable the SSL Plugin on the default.yml by adding it.
     plugins:
     - ssl
     # update python and go versions
     go:
          version: 1.19
     python:
          version: 3.9
     # Consider replacing ( use to test) - /home/$USER/caldera/plugins/ssl/conf/insecure_certificate.pem
     $ sudo openssl req -x509 -nodes -days 1095 -newkey rsa:2048 -keyout /etc/ssl/private/private-ssl.key -out /etc/ssl/certs/private-ssl.crt -subj "/C=US/ST=Any/L=Anytown/O=decyphertek-io/OU=adminotaur/CN=decyphertek"
     $ sudo cat /etc/ssl/certs/private-ssl.crt /etc/ssl/private/private-ssl.key > ~/caldera/plugins/ssl/conf/secured_certificate.pem
     $ vim /home/$USER/caldera/plugins/ssl/templates/haproxy.conf
     bind *:8443 ssl crt plugins/ssl/conf/secured_certificate.pem
     $ sudo systemctl daemon-reload
     $ sudo systemctl restart haproxy
     $ sudo systemctl restart caldera
     # https://ip-of-server:8443

Update Passwords
----------------

     $ vim /home/$USER/caldera/conf/default.yml
     Example:
     users:
       blue:
         blueteam: instance-id

       red:
         redteam: instance-id
     
References
----------

     https://caldera.mitre.org/
     https://caldera.readthedocs.io/en/latest/Installing-CALDERA.html
     https://caldera.readthedocs.io/en/latest/Getting-started.html
     https://caldera.readthedocs.io/en/latest/Plugin-library.html
     