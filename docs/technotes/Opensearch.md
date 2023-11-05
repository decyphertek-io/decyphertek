Opensearch
==========

Opensearch is a fork of Elasticsearch / Kibana 7.10 . Is a a free and opensource alternative to Elastic.co , with some security by default features. 

Install
-------

    # Install Opensearch
    sudo apt update && sudo apt upgrade -y
    sudo apt-get update && sudo apt-get -y install lsb-release ca-certificates curl gnupg2
    # This command appears in two lines, make sure to include them in one.
    curl -o- https://artifacts.opensearch.org/publickeys/opensearch.pgp | sudo gpg --dearmor --batch --yes -o /usr/share/keyrings 
    /opensearch-keyring
    # This command appears in two lines, make sure they are one. 
    echo "deb [signed-by=/usr/share/keyrings/opensearch-keyring] https://artifacts.opensearch.org/releases/bundle/opensearch  
    /2.x/apt stable main" | sudo tee /etc/apt/sources.list.d/opensearch-2.x.list
    sudo apt update && sudo apt install opensearch -y 
    sudo vim /etc/opensearch/opensearch-security/internal_users.yml
    # change reserved: true to reserved: false ( Only on admin , kibanaserver referenced in opensearch_dashboard.yml)
    # Optional: Change the password via hash. ( See command below, not required if reserved:false , can change from GUI. )
    # Optional: Keep in mind reserved:true makes the account immutable. If you need that, then keep it, cant change from GUI.
    
    # Install opensearch-dashboard
    # This command appears in two lines, make sure they are one. 
    curl -o- https://artifacts.opensearch.org/publickeys/opensearch.pgp | sudo gpg --dearmor --batch --yes -o /usr/share/keyrings 
    /opensearch-keyring
    # This command appears in two lines, make sure they are one
    echo "deb [signed-by=/usr/share/keyrings/opensearch-keyring] https://artifacts.opensearch.org/releases/bundle/opensearch- 
    dashboards/2.x/apt stable main" | sudo tee /etc/apt/sources.list.d/opensearch-dashboards-2.x.list
    sudo apt update && sudo apt install opensearch-dashboards -y 
    sudo vim /etc/opensearch-dashboards/opensearch_dashboards.yml
    # uncomment server.port: 5601 
    # uncomment and change server.host: "localhost" to server.host: "0.0.0.0"
    # Issue: If you change the kibanaserver password in internal users, you have to add this to opensearch dashboards config.
    # Issue: Do not use ! points in your password hash generator, since it will call bash history and passwords will not match. 

    # Opensearch 2.x > Java 17 compatible
    sudo apt install openjdk-17-jdk 
    export JAVA_HOME=$(readlink -f /usr/bin/java | sed "s:bin/java::") 
    export OPENSEARCH_JAVA_HOME=$JAVA_HOME 
    java --version 
    echo $JAVA_HOME  
    echo $OPENSEARCH_JAVA_HOME 

    # Start the daemons
    sudo systemctl daemon-reload
    sudo systemctl enable opensearch
    sudo systemctl start opensearch
    sudo systemctl enable opensearch-dashboards
    sudo systemctl start opensearch-dashboards

    # Login ( Can now manage all users from GUI ) 
    http://ip-of-server:5601
    user: admin
    pass: admin
    manage users > management > security > internal users > delete & change passwords

    # Verify opensearch works with new password set:
    curl -XGET -k -u 'admin:NEWPASSWORD' 'https://localhost:9200/_cluster/health?pretty'

    # HTTPS options OpenSearch-Dashboard
    * nginx
    * search guard ( Compatibility unclear 7.10) 
    * Security script process.

    # (Optional) Opensearch Security Script Method:
    # Add your chosen password has to the internal users yml.
    sudo  /usr/share/opensearch/plugins/opensearch-security/tools/hash.sh -p <new-password>

    # Update the Internal users yml
    sudo vim /etc/opensearch/opensearch-security/internal_users.yml

    # Dev certs, to generate your own - https://opensearch.org/docs/latest/security/configuration/generate-certificates/
    # This appears on three lines, except should be one command. 
    sudo /usr/share/opensearch/plugins/opensearch-security/tools/securityadmin.sh -f /etc/opensearch/opensearch-security 
    /internal_users.yml -t internalusers  -icl -nhnv -cacert /etc/opensearch/root-ca.pem -cert /etc/opensearch/kirk.pem -key 
    /etc/opensearch/kirk-key.pem

References
----------

    https://opensearch.org/docs/latest/install-and-configure/install-opensearch/debian/
    https://opensearch.org/docs/latest/security/configuration/generate-certificates/
    