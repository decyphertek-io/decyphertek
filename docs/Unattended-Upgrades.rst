Unattended Upgrades
=====

     Unattended Upgrades is a debian package that automates security patching. 

.. code-block:: console

  ###Unattended Upgrades - Install###
  $ sudo apt install  -y unattended-upgrades apt-listchanges
  $ sudo systemctl enable unattended-upgrades
  $ sudo systemctl start unattended-upgrades
  $ sudo systemctl status unattended-upgrades
  $ sudo dpkg-reconfigure -plow unattended-upgrades | echo "yes"
  $ sudo su -c "curl 'https://raw.githubusercontent.com/decyphertek-io/configs/main/50unattended-upgrades' >> /etc/apt/apt.conf.d/50unattended-upgrades"
  $ sudo apt install -y cron
  $ sudo systemctl enable cron
  $ sudo systemctl start cron
  $ sudo systemctl status cron
  $ (sudo crontab -l ; echo "30 3 * * * /usr/bin/unattended-upgrades -v")| sudo crontab -

  ###Unattended Upgrades - Test### 
  # Crontab runs on a daily schedule, check after a few days. 
  $ cat /var/log/apt/history.log
  

  ###References###
  https://crontab.guru/
  https://wiki.debian.org/UnattendedUpgrades
  https://www.tutorialspoint.com/unix_commands/crontab.htm

