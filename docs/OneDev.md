OneDev
======

All in one CI/CD Platform with a git repo, kanban boards, a code editor, and even integrates email tickets.

Install
-------

    # ubuntu 22.04
    $ sudo apt install -y openjdk-19-jre-headless openjdk-19-jre git curl unzip
    $ export JAVA_HOME=/usr/lib/jvm/java-19-openjdk-amd6
    $ echo $JAVA_HOME
    $ wget https://code.onedev.io/downloads/projects/160/builds/3112/artifacts/onedev-7.7.11.zip
    $ unzip onedev-7.7.11.zip
    $ cd onedev-7.7.11
    $ sudo vim conf/wrapper.conf
    # Comment out  wrapper.java.maxmemory.percent=50
    uncomment wrapper.java.maxmemory=1024
    $ sudo bash bin/server.sh installstart
    $ sudo systemctl status onedev
    # allow inbound access via firewall and security group if required port 6610 
    # https://localhost:6610
    # setup account info 
    # Optional: Setup Nginx Reverse Proxy to route to port 443, see decyphertek nginx docs. 

References
----------

    https://code.onedev.io/projects/160/files
    https://code.onedev.io/projects/162/files/main/pages/installation-guide.md