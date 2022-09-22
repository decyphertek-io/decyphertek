Arkime
=====

Open Source full network packet capture, with visual dashboard. 

Install
--------

     $ wget https://s3.amazonaws.com/files.molo.ch/builds/ubuntu-20.04/arkime_3.4.2-1_amd64.deb
     $ sudo dpkg -i arkime_3.4.2-1_amd64.deb
     # Have Configure script install ElasticSearch
     $ sudo /opt/arkime/bin/Configure
     $ sudo systemctl enable elasticsearch
     $ sudo systemctl start elasticsearch
     # http://ESHOST:9200
     # delete all data - /opt/arkime/db/db.pl
     $ sudo init /opt/arkime/bin/arkime_add_user.sh admin "Admin User" THEPASSWORD --admin
     $ sudo systemctl enable arkimecapture
     $ sudo systemctl start arkimecapture
     $ sudo systemctl enable arkimeviewer
     $ sudo systemctl start arkimeviewer
     # log files
     $ sudo less opt/arkime/logs/viewer.log 
     $ sudo less /opt/arkime/logs/capture.log
     # Login with set user & password 
     # http://arkimeHOST:8005
     # Configs - /opt/arkime/etc/config.ini

     Note:
     # you want IP -> Geo/ASN to work, you need to setup a maxmind account and the geoipupdate program. https://arkime.com/faq#maxmind
     

References
----------

https://arkime.com/
https://arkime.com/faq
https://arkime.com/settings