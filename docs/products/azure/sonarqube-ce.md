SonarQube is an open-source platform for continuous inspection of code quality, helping developers identify and fix bugs and vulnerabilities across multiple programming languages. It provides detailed reports on overall code health, ensuring high standards in software development. Running on Ubuntu 24 LTS with Docker, your SonarQube instance benefits from a containerized environment that simplifies deployment and scaling, while security features like Crowdsec IPS, Auditd Logging, Nginx Reverse Proxy, automated updates, and UFW Host Firewall enhance its protection and stability. [Azure Marketplace: SonarQube CE ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/decyphertek.sonarqube-ce?tab=Overview)


Note:
------
* Please be aware that it takes a few minutes for SonarQube CE to be available. 

SSH Into the server:
--------------------
* Utilize Azure SSH settings to set your ssh keys AND/OR Password to ssh in. 

Sonarqube CE:
-------------
* https://IP-OF-SERVER
* It immediately requires updating password before you can login.
```
username: admin
password: admin
```

Additonal Security Features:
----------------------------
* Crowdsec IPS - https://decyphertek.readthedocs.io/en/latest/technotes/Crowdsec/
* UFW Host Firewall - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Auditd Logging - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Automated Updates - Update script upon first boot and at 3am daily.

References:
-----------
* https://docs.sonarsource.com/sonarqube/latest/