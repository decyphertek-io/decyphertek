Openhab
=====

A smart home that you own and control. Works with most modern smart home tech and is able to utilize multiple platforms.  

OpenHab - Install
------------------

     $ wget -qO - 'https://openhab.jfrog.io/artifactory/api/gpg/key/public' | sudo apt-key add -
     $ echo 'deb https://openhab.jfrog.io/artifactory/openhab-linuxpkg stable main' | sudo tee /etc/apt/sources.list.d/openhab.list
     $ sudo apt-get update
     $ sudo apt-get install openhab openhab-addons

TroubleShooting
----------------

     $ sudo systemctl start openhab.service
     $ sudo systemctl status openhab.service
     $ sudo systemctl daemon-reload
     $ sudo systemctl enable openhab.service

References
----------
  
     https://www.openhab.org/
     https://www.openhab.org/docs/installation/linux.html

