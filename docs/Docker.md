Docker
=====

Docker is a containerization platform that simplifies configs and the deployemnt of 
Enterprise or dev applications. 

Quick Install
-------------

    # Ubuntu ( Will Fail on Debian or other distros )
    $ curl -fsSL https://raw.githubusercontent.com/decyphertek-io/configs/main/bash-scripts/docker.sh | bash
    <OR>
    # Docker's Convience Script Debian
    $ curl -fsSL https://get.docker.com -o get-docker.sh
    $ sudo sh get-docker.sh

Install
-------

    $ sudo apt update
    $ sudo apt-get install ca-certificates curl gnupg lsb-release
    $ sudo mkdir -p /etc/apt/keyrings
    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    $ echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    $ sudo apt-get update
    $ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose docker-compose-plugin
    $ sudo groupadd docker
    $ sudo usermod -aG docker $USER
    $ sudo systemctl enable docker.service
    $ sudo systemctl start docker.service
    # Install docker compose plugin
    $ sudo apt-get install docker-compose-plugin
    # Verify docker-compose plugin
    $ docker compose version
    # May have to logout and back in to avoid docker error.

Optional: Yacht
---------------

    $ docker volume create yacht
    $ docker run -d -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock -v yacht:/config selfhostedpro/yacht
    # Allow 8000 on host/network firewall & Security groups - Example
    $ sudo ufw allow 8000
    # Replace localhost with your IP.
    # http://localhost:8000
    # User: admin@yacht.local Pass: pass
    # Add templates - https://raw.githubusercontent.com/SelfhostedPro/selfhosted_templates/master/Template/yacht.json 

Optional: LinuxServers.io
-------------------------

    https://docs.linuxserver.io/
    https://fleet.linuxserver.io/

Optional: DockStarter
---------------------

    https://dockstarter.com/

Manage Docker
-------------

    # Search a container - Example
    $ docker search ubuntu
    # Download the container
    $ docker pull ubuntu
    # See Running Containers
    $ docker ps
    # See All Containers
    $ docker ps -a
    # See All images
    $ docker images
    # Manage Containers
    $ docker stop CONTAINER_ID
    $ docker start CONTAINER_ID
    $ docker rm CONTAINER_ID

References
----------

    https://docs.docker.com/compose/install/compose-plugin/#install-the-plugin-manually
    https://docs.portainer.io/start/install/server/docker/linux
    https://docs.docker.com/engine/reference/commandline/cli/
    https://docs.docker.com/engine/install/ubuntu/
    https://yacht.sh/docs/Installation/Getting_Started
