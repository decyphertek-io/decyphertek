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
    # Users are stored here:
    $ psql -h localhost -U chirpstack_as -W chirpstack_as
    chirpstack_as=> \dt
    chirpstack_as=> select * from "user";
    # Hashing details -  PBKDF2$sha512$100000
    # Update password via one command - Doesnt Work complex the way they store the password
    # - https://github.com/brocaar/chirpstack-application-server/blob/master/internal/storage/user.go#L214
    # "PBKDF2$" + "sha512$" + "1000$" + "base64.salt" + "$" + "base64.hash"
    # Example Password - PBKDF2$sha512$100000$4u3hL8krvlMIS0KnCYXeMw==$G7c7tuUYq2zSJaUeruvNL/KF30d3TVDORVD56wzvJYmc3muWjoaozH8bHJ7r8zY8dW6Pts2bWyhFfkb/ubQZsA==
    $ sudo -u postgres psql -d chirpstack_as -c "UPDATE public."user" SET password_hash= 'wrong-way-to-update' WHERE email='admin'"

Application Server
--------------------

    $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1CE2AFD36DBCCA00
    $ sudo echo "deb https://artifacts.chirpstack.io/packages/3.x/deb stable main" | sudo tee /etc/apt/sources.list.d/chirpstack.list
    $ sudo apt update
    $ sudo apt install -y chirpstack-application-server
    # Run openssl command to generate api key - save to jwt_secret = 
    $ openssl rand -base64 32
    # Example Config - https://www.chirpstack.io/application-server/install/config/
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
    # Example Config - https://www.chirpstack.io/network-server/install/config/
    $ sudo vim /etc/chirpstack-network-server/chirpstack-network-server.toml
    # Update paramaters / variables
    dsn="postgres://chirpstack_ns:dbpassword@localhost/chirpstack_ns?sslmode=disable"
    automigrate=true
    [network_server]
    # Class C Networks , The first three octets (24 bits / 3 bytes) represent the network ID and the last octet (8 bits / 1 bytes) is the host ID.
    # Example: Private IP = 172.31.26.66 ; Network ID = 172.31.26.0 ; Host ID = 0.0.0.66
    # Encode as Hex - https://convertstring.com/EncodeDecode/HexEncode  = 3137322E33312E32362E30
    # For Class A first octet represents network ID as the prefix of the first octet is 0, it uses the remaining 7 bits for network ID, 
    # Example: Public IP = 107.23.169.36 ; Network ID = 107.0.0.0 ; Host ID = 0.23.169.36
    # Encode as Hex - https://convertstring.com/EncodeDecode/HexEncode = 3130372E302E302E30
    # Github Opened to Clarify this parameter: https://github.com/chirpstack/chirpstack-docs/issues/5
    # Network identifier (NetID, 3 bytes) encoded as HEX (e.g. 010203)
    net_id="000000"
    # Choose from AS923 , AS923-2 , AS923-3 , AS923-4 , AU915 , CN470 , CN779 , EU433 , EU868 
    # IN865 , KR920 , RU864 , US915 , ISM2400 -  https://www.lora-alliance.org/lorawan-for-developers
    [network_server.band]
    name="EU868"
    [metrics]
    # Timezone
    # Example: "Europe/Amsterdam" or "Local" for the the system's local time zone.
    timezone="Local"
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
    # Reboot system to test that all systems start together at reboot
    $ sudo reboot
    # Manage Gateway bridge - Config
    $ sudo vim /etc/chirpstack-gateway-bridge/chirpstack-gateway-bridge.toml
    # Manage Gateway bridge - systemctl 
    $ sudo systemctl [start|stop|restart|status|enable|disable] chirpstack-gateway-bridge
    # Manage Gateway bridge - Logs
    $ sudo journalctl -u chirpstack-gateway-bridge -f -n 50

Getting Started
---------------

    # Example - Customize to your own needs. 
    > Login > Network Servers > ADD > Local-Network-Server , localhost:8000 > Add Network Server
    > Login > Gateway Profiles > Create > Local-Gateway , 30 , 0,1,2 ,  Local-Network-Server >  Create Gateway Profile
    > Login > Service Profiles > Create > Local-Service-Profile , Local-Network-Server , 0 , 0 , 0  > Create Service Profile
    > Login > Gateways > Create > Local-Gateway , description , Gateway ID , Local-Network-Server  , Local-Service-Profile , Local-Gateway , 0 > Create Gateway

Gateway OS
----------

    # Raspberry pi OS that can connect to Chirpstack
    https://www.chirpstack.io/gateway-os/

References
----------

    https://www.chirpstack.io/project/guides/debian-ubuntu/
    https://phoenixnap.com/kb/nginx-reverse-proxy
    https://www.hackster.io/sidikalamini/full-stack-rpi-chirpstack-lorawan-environment-dashboard-f51bd0
    https://www.geeksforgeeks.org/what-is-network-id-and-host-id-in-ip-addresses/