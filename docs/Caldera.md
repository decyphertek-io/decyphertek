Caldera
=====

A Scalable, Automated Adversary Emulation Platform

Install
--------

     $ git clone https://github.com/mitre/caldera.git --recursive 
     $ cd caldera 
     $ sudo apt install python3-pip
     $ sudo -H python3 -m pip install -r requirements.txt
     # Systemd Managed Caldera
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
     # Mange Caldera
     $ sudo systemctl enable caldera
     $ sudo systemctl start caldera
     $ sudo systemctl status caldera
     # Login
     # http://ip-of-server:8888 
     # user = admin
     # password = admin

References
----------

     https://caldera.mitre.org/
     https://caldera.readthedocs.io/en/latest/Installing-CALDERA.html
     https://caldera.readthedocs.io/en/latest/Getting-started.html