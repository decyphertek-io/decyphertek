MeshCentral
=====

"The open source, multi-platform, self-hosted, feature packed web site for remote device management."
WORK IN PROGRESS.... Agents not checking in???

Install
--------

     $ sudo apt update
     $ curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - 
     $ sudo apt-get install -y nodejs 
     $ sudo npm install -g npm@latest
     $ sudo setcap cap_net_bind_service=+ep /usr/bin/node
     $ mkdir ~/meshcentral/
     $ cd ~/meshcentral/
     $ npm install meshcentral
     # Systemd Managed MeshCentral
     $ sudo su -c "curl 'https://raw.githubusercontent.com/decyphertek-io/configs/main/meshcentral.service' >> /etc/systemd/system/meshcentral.service"
     $ sudo systemctl enable meshcentral
     $ sudo systemctl start meshcentral
     $ sudo systemctl status meshcentral
     # https://ip-of-server
     # Login > Create a new account 
     > Add a device Group > Download agent
     # Linux - run generated script as root.
     # Verify the agent checks into the console
     

References
----------

     https://meshcentral.com/info/
     https://github.com/Ylianst/MeshCentral/issues/1076
     https://info.meshcentral.com/downloads/MeshCentral2/MeshCentral2UserGuide.pdf