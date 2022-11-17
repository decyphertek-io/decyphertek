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
     $ mkdir /home/$USER/meshcentral/
     $ cd /home/$USER/meshcentral/
     $ npm install -g meshcentral
     $ npm install -g pm2
     $ pm2 start /home/$USER/meshcentral/node_modules/meshcentral
     $ pm2 save 
     $ pm2 startup
     # Notice output command, run from terminal, then reboot. 
     $ sudo reboot
     $ sudo systemctl status pm2-$USER
     # https://ip-of-server
     # Login > Create a new account 
     > Add a device Group > Download agent
     # Linux - run generated script as root.
     # Verify the agent checks into the console

     # Ports & Protocols
     # Meshagent - Linux listeners
     * 16990
     * 33020
     * 48063
     * 54229
     * 53358
     # Meshcentral - Linux Listeners
     * 80
     * 443
     * 4433 
     * 16990
     
References
----------

     https://meshcentral.com/info/
     https://github.com/Ylianst/MeshCentral/issues/1076
     https://info.meshcentral.com/downloads/MeshCentral2/MeshCentral2UserGuide.pdf