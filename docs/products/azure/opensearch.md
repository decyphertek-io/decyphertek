OpenSearch is an adaptable, scalable open-source platform designed for creating solutions for data-heavy applications. OpenSearch provides features that include search, security, observability, robust performance, developer-friendly tools, and strong integration capabilities.  [Azure Marketplace: OpenSearch ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/decyphertek.opensearch?tab=Overview)

Note:
-----
* Please be patient , it takes 5-10 minutes for OpenSearch to be accessible. 

SSH Into the server:
--------------------
* Utilize Azure to setup user and ssh keys. 
* Make sure to allow ssh, https, & 9443 via network security group.

Passwords:
----------
* To Get the OpenSearch admin Password , run the follwoing command from terminal:
```
sudo cat /root/opensearch_admin_password.txt
```

Login:
------
* login to OpenSearch Dashboard:
```
https://IP-OF-SERVER
Username: admin
Password: (sudo cat /root/opensearch_admin_password.txt )
```

OpenSearch GET/POST:
--------------------
* Example: Check Index Health, cluster check, and post to _doc using curl .
```
# Basic health check
curl -k -u 'admin:PASWORD' "https://IP-OR-DOMAIN:9443/"
# Cluster check
curl -k -u 'admin:PASWORD' "https://IP-OR-DOMAIN:9443/_cluster/health?pretty"
# List all indices
curl -k -u 'admin:PASWORD' "https://IP-OR-DOMAIN:9443/_cat/indices?v"
# Create an index for the data
curl -k -u 'admin:PASSWORD' -X PUT "https://IP-OR-DOMAIN:9443/data"
# Get API data and Post json to _doc
curl -s "https://api.crossref.org/journals?query=pharmacy+health" -H "Accept: application/json" -o health.json
curl -k -u 'admin:PASWORD'  -X POST "https://IP-OR-DOMAIN:9443/data/_doc/" -H "Content-Type: application/json" -d @health.json
# Verify posted data was indexed
curl -k -u 'admin:PASSWORD' "https://IP-OR-DOMAIN:9443/data/_search?pretty"
```

Optional - Nginx:
------
* To change your SSL certs:
```
sudo vim /etc/nginx/conf.d/opensearch.conf
    # Replace with your SSL cert
    ssl_certificate      /etc/ssl/certs/self-signed-crt.pem;
    ssl_certificate_key  /etc/ssl/private/self-signed-key.pem;

sudo nginx -t
sudo systemctl daemon-reload
sudo systemctl reload nginx
sudo systemctl restart nginx
```

Troubleshooting:
----------------
* If you are getting a 502 bad gateway , please wait, opensearch isnt ready yet.
* You can check to see if there are any errors by running systemctl status. 
```
sudo systemctl status opensearch opensearch-dashboards
sudo systemctl start opensearch opensearch-dashboards
```

Security Features:
------------------
* Rsyslog - https://www.rsyslog.com/doc/index.html
* Ossec - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and daily.
* Nginx - https://nginx.org/en/docs/
* Daily Security Report: ( Scheduled via crontab )
```
cd /var/log/decyphertek/
ls
sudo cat security_report_DATE-HERE.log
```

References:
-----------
* https://opensearch.org/docs/latest/