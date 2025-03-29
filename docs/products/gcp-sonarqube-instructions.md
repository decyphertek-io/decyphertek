SonarQube is an open-source platform for continuous inspection of code quality, helping developers identify and fix bugs and vulnerabilities across multiple programming languages. It provides detailed reports on overall code health, ensuring high standards in software development. Running on Flatcar Linux Stable with Docker, your SonarQube instance benefits from a containerized environment that simplifies deployment and scaling, while security features like Crowdsec IPS, Auditd Logging, Nginx Reverse Proxy, automated updates, and UFW Host Firewall enhance its protection and stability. [GCP Marketplace: SonarQube CE ]( https://console.cloud.google.com/marketplace/product/server-build-415714/sonarqube-ce)

Note:
------
* Please be aware that it takes a few minutes for SonarQube CE to be available. 

SSH Into the server:
--------------------
* Utilize OS-Login OR add ssh keys via security & Access > SSH Keys > ssh-rsa KEY core
```
ssh core@ip-of-server
# OR: If using OS Login
sudo su core
cd ~
```

Sonarqube CE:
-------------
* https://IP-OF-SERVER
* It immediately requires updating password before you can login.
```
username: admin
password: admin
```

Security:
---------
* Flatcar Linux - Immutable OS : https://www.flatcar.org/docs/latest/
* Auditd Logging : https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* Nginx: https://nginx.org/en/docs/
* Iptables Firewall : https://linux.die.net/man/8/iptables

References:
-----------
* https://docs.sonarsource.com/sonarqube-community-build/