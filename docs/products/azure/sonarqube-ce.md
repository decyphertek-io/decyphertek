SonarQube is an open-source platform for continuous inspection of code quality, helping developers identify and fix bugs and vulnerabilities across multiple programming languages. It provides detailed reports on overall code health, ensuring high standards in software development. Running on Flatcar Linux with Docker, your SonarQube instance benefits from a secure, containerized environment that simplifies deployment and scaling, with security features like an immutable OS, automatic updates, and Nginx Reverse Proxy ensuring robust protection and stability. [Azure Marketplace: SonarQube CE](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/decyphertek.sonarqube-ce?tab=Overview)


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

References:
-----------
* https://docs.sonarsource.com/sonarqube/latest/