Docker
=====

Docker is a containerization platform that simplifies configs and the deployemnt of 
Enterprise or dev applications. 

Quick Install
-------------

    # Docker's Convience Script Debian
    curl -fsSL https://get.docker.com -o get-docker.sh
    sudo sh get-docker.sh

Install
-------

    sudo apt update
    sudo apt-get install ca-certificates curl gnupg lsb-release
    sudo mkdir -p /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose docker-compose-plugin
    sudo groupadd docker
    sudo usermod -aG docker $USER
    sudo systemctl enable docker.service
    sudo systemctl start docker.service
    # Install docker compose plugin
    sudo apt-get install docker-compose-plugin
    # Verify docker-compose plugin
    docker compose version
    # May have to logout and back in to avoid docker error.

Docker Desktop
---------------

    # Add Docker's official GPG key:
    sudo apt-get update
    sudo apt-get install ca-certificates curl gnupg
    sudo install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    wget -O docker-desktop-4.25.2-amd64.deb "https://desktop.docker.com/linux/main/amd64/docker-desktop-4.25.2-amd64.deb?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-linux-amd64&_gl=1*16ingr4*_ga*MTk5MTE5MjYyMS4xNzAwNjc1MDM4*_ga_XJWPQMJYHQ*MTcwMDY3NTAzOC4xLjEuMTcwMDY3NTIxNi42MC4wLjA."
    sudo dpkg -i docker-desktop-4.25.2-amd64.deb

Manage Docker
-------------

    # run A container example
    docker run -d --name nginx -p 443:443 nginx:latest
    # Search a container - Example
    docker search nginx
    # Download the container
    docker pull nginx
    # See Running Containers
    docker ps
    # See All Containers
    docker ps -a
    # See All images
    docker images
    # Manage Containers
    docker stop CONTAINER_ID
    docker start CONTAINER_ID
    docker rm CONTAINER_ID
    # Enter docker bash shell
    docker exec -it ContainerName bash
    # Execute docker command from terminal
    docker exec -it ContainerName Command

Docker Compose Commands
-----------------------

    # The old way to run docker compose 
    docker-compose up -d
    # Docker Plugin uses docker compose instead of docker-compose
    docker compose build 	    Build or rebuild services
    docker compose convert 	Converts the compose file to platform’s canonical format
    docker compose cp 	    Copy files/folders between a service container and the local filesystem
    docker compose create 	Creates containers for a service.
    docker compose down 	    Stop and remove containers, networks
    docker compose events 	Receive real time events from containers.
    docker compose exec 	    Execute a command in a running container.
    docker compose images 	List images used by the created containers
    docker compose kill 	    Force stop service containers.
    docker compose logs 	    View output from containers
    docker compose ls 	    List running compose projects
    docker compose pause 	    Pause services
    docker compose port 	    Print the public port for a port binding.
    docker compose ps 	    List containers
    docker compose pull 	    Pull service images
    docker compose push 	    Push service images
    docker compose restart 	Restart service containers
    docker compose rm 	    Removes stopped service containers
    docker compose run 	    Run a one-off command on a service.
    docker compose start 	    Start services
    docker compose stop 	    Stop services
    docker compose top 	    Display the running processes
    docker compose unpause 	Unpause services
    docker compose up 	    Create and start containers
    docker compose version 	Show the Docker Compose version information

Optional: UFW & Docker
----------------------

    # Docker bypasses UFW host firewall. There is a fix. 
    sudo wget -O /usr/local/bin/ufw-docker https://github.com/chaifeng/ufw-docker/raw/master/ufw-docker
    sudo chmod +x /usr/local/bin/ufw-docker
    sudo ufw-docker install
    sudo systemctl restart ufw
    # May have to restart Docker or machine as well if issues occur. 
    # Make sure to get the docker name
    docker ps
    # Allow port to docker name
    sudo ufw-docker allow namehere 80/tcp
    # Remove the rule
    sudo ufw-docker delete allow namehere 80/tcp
    # Advanced: Whitelisting
    sudo ufw route allow proto tcp from 1.2.3.4 to any port 9443

Optional: Portainer
-------------------

    docker volume create portainer_data
    docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
    # Allow 9443 on host/network firewall & Security groups - Example
    sudo ufw allow 9443
    # https://localhost:9443
    # Follow setup page instructions
    # If you get a timeout error run:
    docker restart portainer
    # login

Optional: Yacht
---------------

    docker volume create yacht
    docker run -d -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock -v yacht:/config selfhostedpro/yacht
    # Allow 8000 on host/network firewall & Security groups - Example
    sudo ufw allow 8000
    # Replace localhost with your IP.
    # http://localhost:8000
    # User: admin@yacht.local Pass: pass
    # Add templates - https://raw.githubusercontent.com/SelfhostedPro/selfhosted_templates/master/Template/yacht.json 

Optional: Lazy Docker
---------------------

    curl https://raw.githubusercontent.com/jesseduffield/lazydocker/master/scripts/install_update_linux.sh | bash
    # Logout and back in
    lazydocker
    # Follow command prompts listed to manage docker completely from terminal , easily. 

Optional: Gvisor ( Container Security Platform)
----------------

    # https://gvisor.dev/
    sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
    curl -fsSL https://gvisor.dev/archive.key | sudo gpg --dearmor -o /usr/share/keyrings/gvisor-archive-keyring.gpg
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/gvisor-archive-keyring.gpg] https://storage.googleapis.com/gvisor/releases release main" | sudo tee /etc/apt/sources.list.d/gvisor.list > /dev/null
    sudo apt-get update && sudo apt-get install -y runsc
    # If you have Docker installed, it will be automatically configured.

Optional: RacherDesktop
-----------------------

    https://rancherdesktop.io/

Optional: LinuxServers.io
-------------------------

    https://docs.linuxserver.io/
    https://fleet.linuxserver.io/

Optional: DockStarter
---------------------

    https://dockstarter.com/


Optional: Trivy
---------------

    https://github.com/aquasecurity/trivy

References
----------

    https://docs.docker.com/compose/install/compose-plugin/#install-the-plugin-manually
    https://docs.portainer.io/start/install/server/docker/linux
    https://docs.docker.com/engine/reference/commandline/cli/
    https://docs.docker.com/engine/install/ubuntu/
    https://yacht.sh/docs/Installation/Getting_Started
    https://www.howtogeek.com/devops/how-to-use-docker-with-a-ufw-firewall/

