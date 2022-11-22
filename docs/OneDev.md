OneDev
======

All in one Self-hosted Git Server with Kanban and CI/CD . 

Install
-------

    # ubuntu 22.04
    $ sudo apt install -y openjdk-19-jre-headless openjdk-19-jre git curl unzip
    # Install dependencies if install fails.
    $ sudo apt install -f 
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

Terminology
-----------

    Agents - runs on remote machines to execute jobs dispatched by server. It can be included in one 
    or more remote job executors via agent selector. Depending on the job executor being used, it 
    executes jobs either inside or outside containers. Agents are not required if you run jobs on 
    server or inside Kubernetes cluster.

    Job workspace - is the working directory where job commands are executed. Repository and dependency files (if there is any) will be retrieved into this directory. Artifacts/reports will also be published based on this directory

    Steps - are defined in job to execute scripts on designated images. Job steps execute sequentially on job node and share the same job workspace
    
    Step template - groups a sequence of steps as a whole and can be customized with parameters. A step template can be used in a job and itself can use other step templates if necessary

    Services - define live facilities used by a job such as database, message queue etc
    
    Build - is result of running a job
    
    Build Promotion - If some jobs depend on job of a particular build, this build can then be promoted to run these downstream jobs. During promotion, artifacts (normally verified to be good) of current build can be passed to downstream jobs for further processing

    Pipeline - is an execution of job dependency graph. Job dependency graph can be executed by running any job in the graph, either manually or automatically via job triggers

    Build Stream - Two builds are on same stream if they:
    Belongs to same project
    Belongs to same job
    Corresponding commits are on same branch

References
----------

    https://github.com/theonedev/onedev
    https://code.onedev.io/projects/162/files/main/pages/installation-guide.md