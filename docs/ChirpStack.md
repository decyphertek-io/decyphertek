Chirpstack
==========

ChirpStack is an open-source LoRaWAN Network Server which can be used to to setup LoRaWAN networks. 
ChirpStack provides a web-interface for the management of gateways, devices and tenants as well to 
setup data integrations with the major cloud providers, databases and services commonly used for 
handling device data. ChirpStack provides a gRPC based API that can be used to integrate or extend 
ChirpStack.


Requirements
--------------

    $ sudo apt install -y mosquitto postgresql redis-server
    $ sudo systemctl start postgresql@13-main
    $ sudo systemctl enable postgresql@13-main
    $ sudo -u postgres psql 
    create role chirpstack_as with login password 'dbpassword';
    create database chirpstack_as with owner chirpstack_as;
    \c chirpstack_as
    create extension pg_trgm;
    create extension hstore;
    \q
    # Test login : password = dbpassword 
    $ psql -h localhost -U chirpstack_as -W chirpstack_as

Install
-------

    $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1CE2AFD36DBCCA00
    $ sudo echo "deb https://artifacts.chirpstack.io/packages/3.x/deb stable main" | sudo tee /etc/apt/sources.list.d/chirpstack.list
    $ sudo apt update
    $ sudo apt install -y chirpstack-application-server
    # Run openssl command to generate api key - save to jwt_secret = 
    $ openssl rand -base64 32
    $ sudo vim /etc/chirpstack-application-server/chirpstack-application-server.toml
    dsn="postgres://chirpstack_as:dbpassword@localhost/chirpstack_as?sslmode=disable"
    # Example of openssl output to add to jwt_secret
    jwt_secret="HoptoEXT0oKmySPCinatorEYEisSEEnDOGs="
    # Need to change form port 8080 to something else, there is a port conflict 8080 alrady in use. 
    # ip:port to bind the (user facing) http server to (web-interface and REST / gRPC api)
    bind="0.0.0.0:8000"
    $ sudo systemctl enable chirpstack-application-server
    $ sudo apt -y install nginx
    $ sudo systemctl enable nginx
    $ sudo unlink /etc/nginx/sites-enabled/default
    $ sudo mkdir /etc/chirpstack-application-server/certs/
    $ sudo openssl req -x509 -nodes -days 1095 -newkey rsa:2048 -keyout /etc/chirpstack-application-server/certs/http-key.pem -out /etc/chirpstack-application-server/certs/http.pem -subj "/C=US/ST=Any/L=Anytown/O=decyphertek-io/OU=adminotaur/CN=decyphertek"
    $ sudo vim /etc/nginx/sites-enabled/chirpstack.conf
    server {
        listen 443 ssl;
        server_name localhost;

        ssl_certificate /etc/chirpstack-application-server/certs/http.pem;
        ssl_certificate_key /etc/chirpstack-application-server/certs/http-key.pem;

        # WebSocket configuration
        location ~ ^/api/(gateways|devices)/(\w+)/(frames|events)$ {
            proxy_pass http://localhost:8000/api/$1/$2/$3;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "Upgrade";
            proxy_read_timeout 86400s;
            proxy_send_timeout 86400s;
        }

        location / {
            proxy_pass http://localhost:8000/;
        }
    }
    $ sudo systemctl daemon-reload
    $ sudo systemctl start nginx
    $ sudo systemctl start chirpstack-application-server
    # Login https://ip-of-server
    # user - admin pass - admin

Useful Commands
---------------

    # Config
    $ sudo vim  /etc/chirpstack-application-server/chirpstack-application-server.toml
    # Manage Server
    $ sudo systemctl start chirpstack-application-server
    $ sudo systemctl restart chirpstack-application-server
    $ sudo systemctl stop chirpstack-application-server
    # Display Logs
    $ sudo journalctl -f -n 100 -u chirpstack-application-server

Gateway OS
----------

    # Provides an OS to run on Raspberry pi that can connect to Chirpstack
    https://www.chirpstack.io/gateway-os/

References
----------

    https://www.chirpstack.io/project/guides/debian-ubuntu/
    https://pycom.io/chirpstack-a-lorawan-network-server-to-make-you-sing/
    https://phoenixnap.com/kb/nginx-reverse-proxy