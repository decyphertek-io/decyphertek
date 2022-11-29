Jenkins
=======

Automation Pipeline. 

Install
-------

    $ sudo apt install -y openjdk-11-jre git curl && sudo apt install -f 
    $ export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
    $ curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    $ echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
    $ sudo apt-get update && sudo apt-get install -y jenkins
    # Random port conflict on ubuntu,  change HTTP_PORT=8080 to HTTP_PORT=8081
    # If using a proxy  set PREFIX=/jenkins
    $ sudo vim  /etc/default/jenkins
    $ sudo systemctl enable jenkins
    $ sudo systemctl daemon-reload
    # Reboot  system
    # Make sure if you changed the config it loaded.
    $ sudo systemctl status jenkins
    # If change never loads, try $ sudo apt remove jenkins $ sudo apt install jenkins
    # This will keep the config change and upon reinstall load the right port and create the override.conf
    # This override.conf location -  /etc/systemd/system/jenkins.service.d/override.conf
    # This can be edited  $ sudo systemctl edit jenkins
    # Log stored here if any - /var/log/jenkins/jenkins.log
    # http://localhost:8081 or http://localhost:8080
    # Login with admin password and run thru setup. 
    $ sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    # If using nginx reverse proxy review Jenkins docs
    - https://www.jenkins.io/doc/book/system-administration/reverse-proxy-configuration-nginx/
    # After the config is set  and customized, avoid errors
    $ sudo usermod -aG jenkins nginx
    # Setup pam Authentication module to login:
    > Login > manage jenkins > Configure Global Security > Security Realm = Unix user/group database > Save
    # jenkins needs read access on /etc/shadow 
    $ sudo apt-get install nfs4-acl-tools acl
    $ sudo setfacl -m u:jenkins:r /etc/shadow
    # Test out by creating a testuser
    $ sudo useraddd testuser
    $ sudo passwd testuser
    # Login to Jenkins and see if it works.

References
----------

    https://www.jenkins.io/doc/book/installing/linux/#debianubuntu
    https://www.jenkins.io/doc/administration/requirements/upgrade-java-guidelines/