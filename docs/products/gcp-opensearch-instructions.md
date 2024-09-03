OpenSearch is an adaptable, scalable open-source platform designed for creating solutions for data-heavy applications. It provides features like search, security, and observability, coupled with robust performance, developer-friendly tools, and strong integration capabilities.

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

OpenSearch GET/POST:
--------------------
curl -X GET https://IP-OF-SERVER:9443 -u 'admin:YOUR_PASSWORD' --insecure

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

Security Features:
------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and daily.

References:
-----------
* https://opensearch.org/docs/latest/