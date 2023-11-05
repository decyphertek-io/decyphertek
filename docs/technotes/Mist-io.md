Mist-io
=====

Mist is an open source multicloud management platform.

Install {Kubernetes/Helm}
--------------------------

     # Install Microk8s or use eks
     $ helm repo add mist https://dl.mist.io/charts 
     $ helm repo update 
     $ helm install mist-ce mist/mist-ce

Install {Docker}
----------------

     # Install Docker & Docker Compose ( Script works only on Ubuntu - Manually install if using another OS )
     $ curl -fsSL https://raw.githubusercontent.com/decyphertek-io/configs/main/bash-scripts/docker.sh | bash
     # Logout and back in , so changes take effect. 
     $ mkdir mist-io && cd mist-io
     $ wget https://github.com/mistio/mist-ce/releases/download/v4.6.2/docker-compose.yml
     $ docker compose up -d &
     # Make an admin user
     $ docker-compose exec api sh 
     ./bin/adduser --admin admin@example.com
     # Any settings modifications require a restart
     $ sudo vim ./settings/settings.py
     $ docker-compose restart
     # If not localhost, set the PORTAL_URI setting in ./settings/settings.py.
     # Ex: PORTAL_URI = "http://192.168.0.2"
     # See github for additional configurations
     # Or sign up: Hosted mist.io SaaS - https://mist.io/
     

References
-----------

     https://mist.io/
     https://docs.mist.io/
     https://github.com/mistio/mist-ce
     https://github.com/mistio/mist-ce/releases/tag/v4.6.2
     https://docs.mist.io/article/132-ansible-playbooks
     https://github.com/mistio/ansible-examples
     https://docs.docker.com/engine/install/ubuntu/
     https://docs.docker.com/compose/install/
     https://docs.mist.io/article/17-adding-amazon-ec2
     https://docs.mist.io/article/69-what-ports-do-i-need-to-open-for-mist-io

