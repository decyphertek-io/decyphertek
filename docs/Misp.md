MISP
=====

Misp is an open source threat intelligence platform for cyber defense. 

Install
-------
     
     $ sudo apt install -y python3-pip
     $ sudo -H python3 -m pip install pytz -U
     $ sudo -H python3 -m pip install misp-lib-stix2 
     $ sudo useradd -m misp
     $ wget -O /tmp/INSTALL.sh https://raw.githubusercontent.com/MISP/MISP/2.4/INSTALL/INSTALL.sh && bash /tmp/INSTALL.sh -A -D
     $ sudo usermod misp -s /sbin/nologin
     # Watch the terminal regarding password information
     https://ip-of-server
     user: local@admin.test
     Pass: admin

Change the database Passwords
-----------------------------

     # script autogenerates db passwrods stored here > /home/misp/msql.txt
     $ mariadb -u root -p
     maraidb> use mysql;
     mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
     mysql> FLUSH PRIVILEGES;
     mysql> exit
     $ mariadb -u misp -p
     maraidb> use mysql;
     mysql> ALTER USER 'misp'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
     mysql> FLUSH PRIVILEGES;
     mysql> exit
     

Install Options
---------

     -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
     Please specify what type of MISP setup you want to install.
     -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
     /tmp/INSTALL.sh -c | Install ONLY MISP Core
                     -M | MISP modules
                     -m | Mail 2 MISP
                     -S | Experimental ssdeep correlations
                     -A | Install all of the above
     -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
                     -C | Only do pre-install checks and exit
     -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
                     -u | Do an unattended Install, no questions asked
                     -U | Attempt and upgrade of selected item
                     -N | Nuke this MISP Instance
                     -f | Force test install on current Ubuntu LTS schim, add -B for 18.04 -> 18.10, or -BB 18.10 -> 19.10)
     Options can be combined: /tmp/INSTALL.sh -c -D # Will install Core+Dashboard
     -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
     Recommended is either a barebone MISP install (ideal for syncing from other instances) or
     MISP + modules - /tmp/INSTALL.sh -c -M
     Interesting environment variables that get considered are:
     MISP_USER/MISP_PASSWORD # Local username on machine, default: misp/opensslGeneratedPassword
     PATH_TO_MISP # Where MISP will be installed, default: /var/www/MISP (recommended)
     

References
-----------

     https://www.misp-project.org/
     https://misp.github.io/MISP/
     https://www.circl.lu/doc/misp/administration/
     https://www.misp-project.org/misp-training/cheatsheet.pdf
  