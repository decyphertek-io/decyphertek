Crowdsec
=====

     Crowdsec is an open source Intrusion Prevention System that maintains a global IP blacklist. 

.. code-block:: console

  ###Crowdsec - Install###
  $ curl -s https://packagecloud.io/install/repositories/crowdsec/crowdsec/script.deb.sh | sudo bash
  $ sudo apt install -y crowdsec crowdsec-firewall-bouncer-iptables
  $ sudo systemctl enable crowdsec
  $ sudo systemctl start crowdsec
  $ sudo systemctl reload crowdsec
  $ sudo systemctl status crowdsec

  ###Crowdsec - Useful Commands###
  $ sudo cscli collections list
  $ sudo cscli metrics
  $ sudo cscli alerts list
  
  
  ###References###
  https://docs.crowdsec.net/docs/getting_started/install_crowdsec/


