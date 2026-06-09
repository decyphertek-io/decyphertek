OpenSearch is an adaptable, scalable open-source platform designed for creating solutions for data-heavy applications. OpenSearch provides features that include search, security, observability, robust performance, developer-friendly tools, and strong integration capabilities.  [Azure Marketplace: OpenSearch ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/decyphertek.opensearch?tab=Overview)

Note:
-----
* Please be patient , it takes 5-10 minutes for OpenSearch to be accessible. 
* After 06/26 admin user is no longer used
* The old password path before 06/26 /root/opensearch_admin_password.txt

SSH Into the server:
--------------------
* Utilize Azure to setup user and ssh keys. 
* Make sure to allow ssh, https, & 9443 via network security group.

Hardening Changes:
------------------
* Starting with version 3.6.0, this image ships hardened by default:
    * The OpenSearch Security demo configuration has been fully removed.
    * The internal user database has been reduced to only the accounts required for operation
      (`adminotaur` for administration and `kibanaserver` for the Dashboards service account).
    * Self-signed TLS certificates and all account passwords are generated uniquely on first boot,
      so no two deployments share the same credentials or keys.

Passwords:
----------
* To Get the OpenSearch admin Password , run the follwoing command from terminal:
```
# The new path after 06/26
sudo cat /root/opensearch-credentials.txt
```

Login:
------
* login to OpenSearch Dashboard:
```
https://IP-OF-SERVER
Username: adminotaur
Password: (sudo cat /root/opensearch-credentials.txt )
```

OpenSearch GET/POST:
--------------------
* The default `admin` user has been replaced with `adminotaur`. Examples:
```
# Basic health check
curl -k -u 'adminotaur:PASSWORD' "https://IP-OR-DOMAIN:9443/"
# Cluster check
curl -k -u 'adminotaur:PASSWORD' "https://IP-OR-DOMAIN:9443/_cluster/health?pretty"
# List all indices
curl -k -u 'adminotaur:PASSWORD' "https://IP-OR-DOMAIN:9443/_cat/indices?v"
# Create an index for the data
curl -k -u 'adminotaur:PASSWORD' -X PUT "https://IP-OR-DOMAIN:9443/data"
# Get API data and Post json to _doc
curl -s "https://api.crossref.org/journals?query=pharmacy+health" -H "Accept: application/json" -o health.json
curl -k -u 'adminotaur:PASSWORD' -X POST "https://IP-OR-DOMAIN:9443/data/_doc/" -H "Content-Type: application/json" -d @health.json
# Verify posted data was indexed
curl -k -u 'adminotaur:PASSWORD' "https://IP-OR-DOMAIN:9443/data/_search?pretty"
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