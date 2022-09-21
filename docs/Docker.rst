Docker
=====

     Docker is a containerization platform that simplifies configs and the deployemnt of 
     Enterprise or dev applications. 

.. code-block:: console

  ###Docker & Docker Compose - Install##
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


  ###References###
  https://docs.docker.com/engine/install/ubuntu/
  https://docs.docker.com/compose/install/compose-plugin/#install-the-plugin-manually
