Chirpstack
==========

ChirpStack is an open-source LoRaWAN Network Server which can be used to to setup LoRaWAN networks. 
ChirpStack provides a web-interface for the management of gateways, devices and tenants as well to 
setup data integrations with the major cloud providers, databases and services commonly used for 
handling device data. ChirpStack provides a gRPC based API that can be used to integrate or extend 
ChirpStack.

Requirements
--------------

    # Install Requirements for Application, Gateway, and Network server.
    $ sudo apt install -y mosquitto postgresql redis-server
    $ sudo systemctl enable redis-server
    $ sudo systemctl start redis-server
    $ sudo systemctl enable postgresql@13-main
    $ sudo systemctl start postgresql@13-main
    $ sudo -u postgres psql 
    create role chirpstack_as with login password 'dbpassword';
    create database chirpstack_as with owner chirpstack_as;
    create role chirpstack_ns with login password 'dbpassword';
    create database chirpstack_ns with owner chirpstack_ns;
    \c chirpstack_as
    create extension pg_trgm;
    create extension hstore;
    \q
    # Test login : password = dbpassword 
    $ psql -h localhost -U chirpstack_as -W chirpstack_as
    $ psql -h localhost -U chirpstack_ns -W chirpstack_ns

Application Server
--------------------

    $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1CE2AFD36DBCCA00
    $ sudo echo "deb https://artifacts.chirpstack.io/packages/3.x/deb stable main" | sudo tee /etc/apt/sources.list.d/chirpstack.list
    $ sudo apt update
    $ sudo apt install -y chirpstack-application-server
    # Run openssl command to generate api key - save to jwt_secret = 
    $ openssl rand -base64 32
    $ sudo vim /etc/chirpstack-application-server/chirpstack-application-server.toml
    dsn="postgres://chirpstack_as:dbpassword@localhost/chirpstack_as?sslmode=disable"
    # Need to change form port 8080 to something else, there is a port conflict 8080 alrady in use. 
    # ip:port to bind the (user facing) http server to (web-interface and REST / gRPC api)
    bind="0.0.0.0:8333"
    # Example of openssl output to add to jwt_secret
    jwt_secret="HoptoEXT0oKmySPCinatorEYEisSEEnDOGs="
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
            proxy_pass http://localhost:8333/api/$1/$2/$3;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "Upgrade";
            proxy_read_timeout 86400s;
            proxy_send_timeout 86400s;
        }

        location / {
            proxy_pass http://localhost:8333/;
        }
    }
    $ sudo systemctl daemon-reload
    $ sudo systemctl start nginx
    $ sudo systemctl start chirpstack-application-server
    $ sudo reboot
    # Login https://ip-of-server
    # user - admin pass - admin
    # Change admin password upon login.
    > Login > All Users > admin > change password > Update password
    # Create Additonal Users
    > Login > All Users > Create > Add info > Create User
    # manage server
    $ sudo systemctl [start|stop|restart|status|enable|disable] chirpstack-application-server
    # Config
    $ sudo vim /etc/nginx/sites-enabled/chirpstack.conf
    # Display Logs
    $ sudo journalctl -f -n 100 -u chirpstack-application-server

Network Server
--------------

    # Can skip adding key if already added from application server install.
    $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1CE2AFD36DBCCA00
    $ sudo echo "deb https://artifacts.chirpstack.io/packages/3.x/deb stable main" | sudo tee /etc/apt/sources.list.d/chirpstack.list
    $ sudo apt update
    $ sudo apt install chirpstack-network-server
    $ sudo vim /etc/chirpstack-network-server/chirpstack-network-server.toml
    # Update paramaters
    dsn="postgres://chirpstack_ns:dbpassword@localhost/chirpstack_ns?sslmode=disable"
    postgresql.automigrate
    network_server.net_id
    network_server.band.name
    metrics.timezone
    $ sudo systemctl enable chirpstack-network-server
    $ sudo systemctl start chirpstack-network-server
    # Manage Network Server - Config 
    $ sudo vim /etc/chirpstack-network-server/chirpstack-network-server.toml
    # Manage Network server - systemctl 
    $ sudo systemctl [start|stop|restart|status|enable|disable] chirpstack-network-server
    # Manage Network server - Display Logs
    $ sudo journalctl -f -n 100 -u chirpstack-network-server

Gateway Bridge
-------------

    # Can skip adding key if already added from application server install.
    $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1CE2AFD36DBCCA00
    $ sudo echo "deb https://artifacts.chirpstack.io/packages/3.x/deb stable main" | sudo tee /etc/apt/sources.list.d/chirpstack.list
    $ sudo apt update
    $ sudo apt install chirpstack-gateway-bridge
    $ sudo systemctl enable chirpstack-gateway-bridge
    $ sudo systemctl start chirpstack-gateway-bridge
    # Manage Gateway bridge - Config
    $ sudo vim /etc/chirpstack-gateway-bridge/chirpstack-gateway-bridge.toml
    # Manage Gateway bridge - systemctl 
    $ sudo systemctl [start|stop|restart|status|enable|disable] chirpstack-gateway-bridge
    # Manage Gateway bridge - Logs
    $ sudo journalctl -u chirpstack-gateway-bridge -f -n 50
   

Getting Started
---------------

    > Login > Network Servers > ADD > Local-Network-Server , localhost:8000 > Add Network Server
    > Login > Gateway Profiles > Create > Local-Gateway , 30 , 0,1,2 ,  Local-Network-Server >  Create Gateway Profile

Gateway OS
----------

    # Raspberry pi OS that can connect to Chirpstack
    https://www.chirpstack.io/gateway-os/

References
----------

    https://www.chirpstack.io/project/guides/debian-ubuntu/
    https://pycom.io/chirpstack-a-lorawan-network-server-to-make-you-sing/
    https://phoenixnap.com/kb/nginx-reverse-proxy