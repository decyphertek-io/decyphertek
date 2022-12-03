MeshCentral
=====

"The open source, multi-platform, self-hosted, feature packed web site for remote device management."

Install
--------

     $ sudo apt update
     $ sudo su -c "curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -"
     $ curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - 
     $ sudo apt-get install -y nodejs 
     $ mkdir ~/.npm
     $ npm config set prefix ~/.npm
     $ export PATH="$PATH:$HOME/.npm/bin"
     $ source ~/.bashrc
     $ npm install -g npm@latest
     $ sudo setcap cap_net_bind_service=+ep /usr/bin/node
     $ mkdir meshcentral && cd meshcentral
     $ npm install meshcentral
     $ node /home/$USER/meshcentral/node_modules/meshcentral --install
     $ sudo systemctl status meshcentral
     # https://ip-of-server
     # Login > Create a new account 
     > Add a device Group > Download agent
     # Linux - run generated script as root.
     $ sudo systemctl status meshagent
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