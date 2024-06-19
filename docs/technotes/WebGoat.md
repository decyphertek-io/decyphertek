WebGoat
=====

OWASP WebGoat is a vulnerable server to practice security testing. 

Install
-------

    # Install docker
    docker run -it -p 127.0.0.1:8080:8080 -p 127.0.0.1:9090:9090 -e TZ=America/Los_Angeles webgoat/webgoat
    # http://localhost:8080/WebGoat 
    # Note: 
    To change the IP address add the following variable to the WebGoat/webgoat-container/src/main/resources/application.properties file:
    server.address=x.x.x.x


References
----------

    https://github.com/WebGoat/WebGoat
    https://owasp.org/www-project-webgoat/