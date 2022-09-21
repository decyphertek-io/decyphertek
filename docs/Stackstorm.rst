Stackstorm
=====

     Stackstorm is an open source event driven automation platform that can automate your enterprise infrastructure. 

.. code-block:: console

  ###Stack Storm - install###
  $ bash <(curl -sSL https://stackstorm.com/packages/install.sh) --user=st2admin --password=Ch@ngeMe  
  $ sudo htpasswd /etc/st2/htpasswd st2admin 
  $ sudo st2ctl restart 
  # Change password
  $ sudo htpasswd /etc/st2/htpasswd st2admin
  # Manage server apply changes
  $ sudo st2ctl restart
  
  
  ###References###
  https://docs.stackstorm.com/
  https://docs.stackstorm.com/install/index.html 
  https://docs.stackstorm.com/authentication.html 

