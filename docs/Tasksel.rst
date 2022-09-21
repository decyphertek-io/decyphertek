Tasksel
=====

  Taskel can easily install server requirements, including a web server, db server, mail server, etc.

.. code-block:: console

  ###Taskel - Example###
  $ sudo  tasksel --task-packages web-server 
  # EX: Packages Installed
  # libapache2-mod-python apache2-doc libapache2-mod-php5 libapache2-mod-perl2 apache2-mpm-prefork analog
  $ sudo sudo  tasksel --task-packages package-name-here
  # Package Options
  * desktop
  * web-server 
  * print-server 
  * dns-server 
  * file-server 
  * mail-server 
  * database-server 
  * ssh-server 
  * laptop 
  * manual 


  ###References###
  https://wiki.debian.org/tasksel