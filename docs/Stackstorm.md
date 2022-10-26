Stackstorm
=====

Stackstorm is an open source event driven automation platform that can automate your enterprise infrastructure. 

Install
-------

     # Ubuntu 20.04 
     $ sudo apt update && sudo apt upgrade
     $ sudo apt install net-tools
     $ bash <(curl -sSL https://stackstorm.com/packages/install.sh) --user=st2admin --password=Ch@ngeMe  

     # Currently getting this error:
     The following packages have unmet dependencies:
     rabbitmq-server : Depends: erlang-base (>= 1:25.0) but 1:24.3.4.6-1 is to be installed or
                                erlang-base-hipe (>= 1:25.0) but it is not going to be installed or
                                esl-erlang (>= 1:25.0) but it is not installable
     # Opened an issue on github regarding:
     - https://github.com/StackStorm/st2docs/issues/1149

     $ sudo htpasswd /etc/st2/htpasswd st2admin 
     $ sudo st2ctl restart 
     # Change password
     $ sudo htpasswd /etc/st2/htpasswd st2admin
     # Manage server apply changes
     $ sudo st2ctl restart

Manage Your Databases
---------------------


  
References
----------

     https://docs.stackstorm.com/
     https://docs.stackstorm.com/install/index.html 
     https://docs.stackstorm.com/authentication.html 
     https://docs.stackstorm.com/install/u20.html

