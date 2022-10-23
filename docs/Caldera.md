Caldera
=====

A Scalable, Automated Adversary Emulation Platform

Install
--------

     $ git clone https://github.com/mitre/caldera.git --recursive 
     $ cd caldera 
     $ sudo apt install python3-pip
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

Setup SSL Cert
--------------

     # These Instructions do not work, Work in progress.....
     $ sudo apt install haproxy
      > Login > Configuration > Plugins > SSL = Enabled
     > Login > Configuration > Setting Name > app.contact.http = https://0.0.0.0:8443 > Update
     $ mv /home/$USER/caldera/plugins/ssl/conf/insecure_certificate.pem /home/$USER/caldera/plugins/ssl/conf/insecure_certificate.pem.bak
     $ sudo openssl req -x509 -nodes -days 1095 -newkey rsa:2048 -keyout /home/$USER/caldera/plugins/ssl/conf/ssl.pem -out /home/$USER/caldera/plugins/ssl/conf/cert.pem -subj "/C=US/ST=Any/L=Anytown/O=decyphertek-io/OU=adminotaur/CN=decyphertek"
     $ sudo systemctl daemon-reload
     $ sudo systemctl restart caldera
     # https://ip-of-server:8443


References
----------

     https://caldera.mitre.org/
     https://caldera.readthedocs.io/en/latest/Installing-CALDERA.html
     https://caldera.readthedocs.io/en/latest/Getting-started.html
     https://www.blackhillsinfosec.com/how-to-install-mitre-caldera-and-configure-your-ssl-certificate/