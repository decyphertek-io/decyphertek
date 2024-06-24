Gray Log
=====

GreyLog is an open source log managment platform with Enterprise options. 

Install
-------

     sudo add-apt-repository universe
     sudo apt update && sudo apt upgrade
     sudo apt install -y apt-transport-https openjdk-<version_number>-jre-headless uuid-runtime pwgen
     # MongoDB
     sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
     echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
     sudo apt update
     sudo apt install -y mongodb-org
     sudo systemctl daemon-reload
     sudo systemctl enable mongod.service
     sudo systemctl restart mongod.service
     sudo systemctl --type=service --state=active | grep mongod
     # ElasticSearch
     wget -q https://artifacts.elastic.co/GPG-KEY-elasticsearch -O myKey
     sudo apt-key add myKey
     echo "deb https://artifacts.elastic.co/packages/oss-7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
     sudo apt-get update && sudo apt-get install elasticsearch-oss
     sudo tee -a /etc/elasticsearch/elasticsearch.yml 
     cluster.name: graylog 
     action.auto_create_index: false 
     sudo systemctl daemon-reload
     sudo systemctl enable elasticsearch.service
     sudo systemctl restart elasticsearch.service
     sudo systemctl --type=service --state=active | grep elasticsearch
     # GreyLog Install
     wget https://packages.graylog2.org/repo/packages/graylog-4.3-repository_latest.deb
     sudo dpkg -i graylog-4.3-repository_latest.deb
     sudo apt-get update && sudo apt-get install graylog-server 

     # Notes:
     Read the instructions within the configurations file and edit as needed, located at /etc/graylog/server/server.conf. Additionally, 
     # add password_secret and root_password_sha2 as these are mandatory and Graylog will not start without them.
     # To create your root_password_sha2 run the following command:
     echo -n "Enter Password: " && head -1 </dev/stdin | tr -d '\n' | sha256sum | cut -d" " -f1
     # Public access set
     http_bind_address to the public hostname

Manage Deamons
--------------

     sudo systemctl daemon-reload
     sudo systemctl enable graylog-server.service
     sudo systemctl start graylog-server.service
     sudo systemctl --type=service --state=active | grep graylog

Server.conf
-----------

     https://docs.graylog.org/docs/server-conf

Syslog
------

     https://www.rsyslog.com/windows-agent/
     https://www.howtoforge.com/how-to-send-ubuntu-logs-to-graylog-server/

Sidecar Install
----------------

     https://docs.graylog.org/docs/sidecar

MongoDB Replica Set
-------------------

     https://www.mongodb.com/docs/manual/tutorial/deploy-replica-set/
     https://docs.graylog.org/docs/multinode-setup

Palo Alto + Fortigate
---------------------

     https://docs.graylog.org/docs/palo-alto
     https://docs.graylog.org/docs/fortigate

Plugins
-------

     https://community.graylog.org/t/active-directory-auditing-winlogbeats-graylog-3-0-2/22889
     https://community.graylog.org/search?context=category&context_id=31&q=Palo%20alto&skip_context=true

  
  
References
----------

     https://www.graylog.org/
     https://docs.graylog.org/docs/ubuntu
     https://docs.graylog.org/docs/sidecar
     https://kelley.jodymaroni.com/windows-filebeat-configuration-and-graylog-sidecar-the-graylog-blog/
     https://www.graylog.org/features/fault-tolerance
     https://docs.graylog.org/docs/server-conf
     https://docs.graylog.org/docs/multinode-setup
     https://www.mongodb.com/docs/manual/tutorial/deploy-replica-set/