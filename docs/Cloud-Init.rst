Cloud Init
=====

     CLoud Init can be used by all Linux systems to customize builds in all cloud platforms. 

.. code-block:: console

  ###Cloud Init -  Install & Utilize###
  # Interactive
  $ sudo apt install cloud-init
  $ sudo dpkg-reconfigure cloud-init
  <OR>
  $ sudo vim /etc/cloud/cloud.cfg
  # Change ubuntu to the username you want. 
  
  system_info:
   # This will affect which distro class gets used
   distro: ubuntu
   # Default user name + that default users groups (if added/used)
   default_user:
     name: ubuntu
     lock_passwd: True
     gecos: Ubuntu

  $ sudo cloud-init clean --logs
  $ sudo cloud-init init --local
  $ sudo cloud-init init
  $ sudo cloud-init modules --mode=config
  $ sudo cloud-init modules --mode=final
  # On a server build , the ubuntu user still exisits. Lets change that
  $ sudo pkill -KILL -u ubuntu
  $ sudo deluser ubuntu
  $ sudo rm -rf /home/ubuntu


  ###References###
  https://cloud-init.io/
  https://www.digitalocean.com/community/tutorials/how-to-use-cloud-config-for-your-initial-server-setup
  https://stackoverflow.com/questions/23065673/how-to-re-run-cloud-init-without-reboot
