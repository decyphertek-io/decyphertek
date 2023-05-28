Dependency Track
=====

Dependency Track is an open source SBOM ( Software Bill Of Materials) OWASP project, 
that can help find vulnerabilites in your open source projects. 

Install
-------

     # Install Docker & Docker Compose - ubuntu script
     $ curl -fsSL https://raw.githubusercontent.com/decyphertek-io/configs/main/bash-scripts/docker.sh | bash
     $ mkdir dependencytrack && cd dependencytrack
     $ wget https://dependencytrack.org/docker-compose.yml
     $ docker compose up -d

References
----------

     https://dependencytrack.org/
