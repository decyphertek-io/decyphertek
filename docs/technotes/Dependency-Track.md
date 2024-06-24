Dependency Track
=====

Dependency Track is an open source SBOM ( Software Bill Of Materials) OWASP project, 
that can help find vulnerabilites in your open source projects. 

Install
-------

     # Install Docker & Docker Compose - ubuntu script
     curl -fsSL https://raw.githubusercontent.com/decyphertek-io/configs/main/bash-scripts/docker.sh | bash
     # Logout & back in for docker group permissions to work. 
     mkdir dependencytrack && cd dependencytrack
     wget https://dependencytrack.org/docker-compose.yml
     docker compose up -d
     # Port conflict on ubuntu 22.04 , not sure why Ubuntu uses 8080 now? 
     # When I try to update docker-compose to 8082 , it listens via netstat, doesnt appear to work?
     ------
     OR
     -----
     # Pull the image from the Docker Hub OWASP repo
     docker pull dependencytrack/bundled
     # Creates a dedicated volume where data can be stored outside the container
     docker volume create --name dependency-track
     # Run the bundled container with 8GB RAM on port 8082
     docker run -d -m 8192m -p 8082:8082 --name dependency-track -v dependency-track:/data dependencytrack/bundled

References
----------

     https://dependencytrack.org/
