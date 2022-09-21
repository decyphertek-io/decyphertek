Quad9
=====

     Quad9 provides DNS security via encrypted DNS queries, blocking malicous domains and botnets by default.  

.. code-block:: console

  ###Quad9 - Install###
  $ sudo add-apt-repository universe && sudo apt update 
  $ sudo apt install -y stubby resolvconf network-manager lynx
  $ sudo mv /etc/stubby/stubby.yml /etc/stubby/stubby.backup.yml && sudo wget -O /etc/stubby/stubby.yml https://support.quad9.net/hc/en-us/article_attachments/4411087149453/stubby.yml
  $ sudo systemctl enable --now resolvconf.service
  $ sudo su -c "echo 'nameserver 127.0.0.1' >> /etc/resolvconf/resolv.conf.d/head"
  $ sudo resolvconf -u
  $ sudo systemctl restart systemd-resolved.service && sudo systemctl restart network-manager 
  $ sudo service stubby restart

  ###Quad9 - Test###
  $ lynx https://on.quad9.net/
  
  
  ###References###
  https://askubuntu.com/questions/1280277/how-to-change-dns-server-permanently-on-ubuntu-20-04
  https://support.quad9.net/hc/en-us/articles/4409217364237-DNS-over-TLS-Ubuntu-18-04-20-04-Stubby-
  https://www.techrepublic.com/article/how-to-use-dns-over-tls-on-ubuntu-linux/

