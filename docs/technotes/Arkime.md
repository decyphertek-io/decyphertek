Arkime
=====

Open Source full network packet capture, with visual dashboard. 

Install
--------

     # Ubuntu 22.04 LTS 
     $ wget https://github.com/arkime/arkime/releases/download/v5.0.0-rc3/arkime_5.0.0-rc3-1.ubuntu2204_amd64.deb
     $ sudo dpkg -i arkime_5.0.0-rc3-1.ubuntu2204_amd64.deb
     # Have Configure script install ElasticSearch
     $ sudo /opt/arkime/bin/Configure
     $ sudo systemctl enable elasticsearch
     $ sudo systemctl start elasticsearch
     $ sudo /opt/arkime/db/db.pl http://127.0.0.1:9200 init
     $ sudo /opt/arkime/db/db.pl http://127.0.0.1:9200 upgrade
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