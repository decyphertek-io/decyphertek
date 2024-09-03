OpenSearch is a flexible, scalable, open-source way to build solutions for data-intensive applications. It offers search, security, observability, and more features, with built-in performance, developer-friendly tools, and powerful integrations.

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

Security Features:
------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and daily.

References:
-----------
* https://opensearch.org/docs/latest/