OpenSearch is an adaptable, scalable open-source platform designed for creating solutions for data-heavy applications. OpenSearch provides features that include search, security, observability, robust performance, developer-friendly tools, and strong integration capabilities. [GCP Marketplace: OpenSearch ](https://console.cloud.google.com/marketplace/product/server-build-415714/opensearch)

Note:
-----
* Please be patient , it takes 5-10 minutes for OpenSearch to be accessible. 

SSH:
----
* Utilize Google SSH Console or setup ssh keys or password.

Passwords:
----------
* To Get the OpenSearch admin Password , run the follwoing command from terminal:
```
sudo cat /home/adminotaur/opensearch_admin_password.txt
```

Login:
------
* login to OpenSearch Dashboard:
```
https://IP-OF-SERVER
Username: admin
Password: (sudo cat /home/adminotaur/opensearch_admin_password.txt )
```

(optional) Opensearch Settings:
------------------------------
* opensearch Config (Setup to use nginx, changes may break that)
```
sudo vim /etc/opensearch/opensearch.yml
```
* Sets java heap size. This can break Opensearch, please proceed with caution.
```
sudo vim /etc/opensearch/jvm.options
# Limit set to 4gb
-Xms4g
-Xmx4g

sudo systemctl daemon-reload
sudo systemctl restart opensearch
```


OpenSearch GET/POST:
--------------------
* GET Using curl:
```
curl -X GET https://IP-OF-SERVER:9443 -u 'admin:PASSWORD' --insecure

```
* Install httpie terminal or Desktop 
    * https://httpie.io/cli
    * https://httpie.io/desktop
* HTTPIE Linux Terminal Example:
```
# GET/POST Example using HTTPIE & health.json
# Basic GET no auth example ( https://mixedanalytics.com/blog/list-actually-free-open-no-auth-needed-apis/)
http --pretty=format GET "https://api.crossref.org/journals?query=pharmacy+health" "Accept:application/json"  >> health.json
# If using auth for an API > http --pretty=format GET "https://example.com" "Authorization:Bearer $API_KEY" "Accept:application/json"  >> example.json
# Create an index > Opensearch Dashboard > Index Managment > Indexes > Create index > EX: health
# Test the index 
http --verify=no --auth admin:your_password GET https://IP-OR-DOMAIN:9443/health/
http --verify=no --auth admin:your_password POST https://IP-OR-DOMAIN:9443/health/_doc/ Content-Type:application/json < health.json
# Create Index Pattern > Dashboard > Managment > Dashboard Managment > Create Index Pattern > health*
# You can now discover the data & Create Dashboards.
```
* Note this is just an example, please utilize your own API or json data to get customized results. 
* Can be useful if you need to pull in data from multiple APIs and crossreference the data. 

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
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and daily.

References:
-----------
* https://opensearch.org/docs/latest/