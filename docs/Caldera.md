Caldera
=====

A Scalable, Automated Adversary Emulation Platform

Install
--------

     $ git clone https://github.com/mitre/caldera.git --recursive 
     $ cd caldera 
     $ sudo apt install python3-pip
     $ sudo -H python3 -m pip install -r requirements.txt
     $ sudo python3 server.py --insecure
     # http://localhost:8888 with the
     # user = admin
     # password = admin
     # Systemd Managed Caldera
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
     # Mange Caldera
     $ sudo systemctl enable caldera.service
     $ sudo systemctl start caldera.service
     $ sudo systemctl status caldera.service


References
----------

     https://caldera.mitre.org/
     https://caldera.readthedocs.io/en/latest/Installing-CALDERA.html
     https://caldera.readthedocs.io/en/latest/Getting-started.html