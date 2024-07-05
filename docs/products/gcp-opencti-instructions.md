OpenCTI is an open-source platform designed to facilitate the collection, storage, and dissemination of cyber threat intelligence. 
It offers a structured environment for the analysis and sharing of technical and non-technical information, enhancing an organization's 
ability to understand and respond to cybersecurity threats. With its user-friendly interface and robust integrations, OpenCTI is an 
essential tool for cybersecurity professionals seeking to streamline their intelligence operations.

Note:
-----
* Opencti Requires at least 4cpu + 16GB RAM + 20GB storage. e2-standard-4 vm or larger is required. 
* Please allow up to 10 minutes for OpenCTI to be accessible. 
* Dashboards takes up to 30-60 minutes to pull in data and populate the visuals.
* I have set basic connectors - Mitre, CISA , Threafox , and some internal enrichment.
* To see the data ingestion progress > Data > Ingestion > Connectors 

SSH Into the server:
--------------------
* Utilize Google SSH Console or setup ssh keys or password.

Passwords - DB AND/OR User:
----------------------------
* ssh into server:
```
sudo cat /home/adminotaur/.docker/.env
```
* This will display the randomly generated passwords for DB AND/OR User. 

OpenCTI CE:
-----------
* Login > https://ip-of-server   username: admin@opencti.io  Password: ( From terminal run : sudo cat /home/adminotaur/.docker/.env | grep OPENCTI_ADMIN_PASSWORD )
* Please be patient, If you access too early you may get a 502 gateway error, since OpenCTI isnt ready yet.

Add an OpenCTI connector:
------------------------
* You can add a connector without bringing down Opencti and can just add to it. 
```
sudo su adminotaur
cd ~/.docker/connectors-6.1.12/external-import/{Connector-Name-HERE}
vim docker-compose.yml
```
* Change the following in Environment and add API Key / User / Password if required ( Add Container Name to easily manage / Troubleshoot . )
* Get Opencti Admin Token:
```
cat ~/.docker/.env | grep OPENCTI_ADMIN_TOKEN
```
* Generate a UUID:
```
cat /proc/sys/kernel/random/uuid
```
* Example docker-compose.yml:
```
container_name: CUSTOM-NAME-HERE
environment:
  - OPENCTI_URL=http://opencti:8080
  - OPENCTI_TOKEN=Run_Command_above_to_Get_Token
  - CONNECTOR_ID=GENERATE_A_RANDOM_UUID
```
* Make sure to Add it to the Network > Opencti-net:
```
restart: always
networks:
  docker_opencti-net:
```
* Also, add networks at the end of the docker-compose.yml
```
networks:
  docker_opencti-net:
    external: true
```
* Once those parameters are changed and added run:
```
docker compose up -d
```
* Check Connector > Login > Data > Ingestion > Connectors > look for the new connector
* From Terminal: If you have issues run:
```
docker logs CUSTOM-NAME-HERE 
```

Enabled Rss Feeds:
------------------
* Data > Ingestion > Rss Feeds > Add your rss feed > Once created > Click on right side , three buttons > Start

Portainer - Manage Docker:
--------------------------
* How to access Portainer to manage your containers > https://ip-of-server:9443
* Follow the instructions to create a new admin account. 
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server:
```
sudo su adminotaur
docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here. 

References:
------------
* https://docs.docker.com/
* https://docs.portainer.io/
* https://docs.opencti.io/latest/


