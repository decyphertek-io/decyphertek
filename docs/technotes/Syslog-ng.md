Syslog-ng is a for of Rsyslog and provides a more modern approach, with more verbose documentation.

Install & Setup Instructions:
-----------------------------

    # This is example is for Amazon Linux / Wazuh found on AWS Marketplace
    $ sudo amazon-linux-extras install epel -y
    $ sudo yum install syslog-ng
    $ cd /etc/syslog-ng/
    # Follow interactactive setup
    $ sudo openssl req -newkey rsa:2048 -nodes -keyout key.pem -out request.csr
    $ sudo openssl x509 -req -days 365 -in request.csr -signkey key.pem -out server-cert.pem
    >>> Upload server-cert.pem to SaaS you want to forward syslog form Once syslog-ng has been started . 
    $ sudo touch /var/log/syslog-ng.log
    $ sudo vim syslog-ng.conf

    # Keep default config and add the following. 
    # TLS Config
    source s_network_tls {
        network(
            transport("tls")
            port(514)  # Specify the port to listen on for TLS connections
            tls(
                key-file("/etc/syslog-ng/key.pem")
                cert-file("/etc/syslog-ng/server-cert.pem")
                peer-verify(optional-untrusted) 
            )
        );
    };

    destination d_tls_logs {
        file("/var/log/syslog-ng.log"); # Path to save the logs received over TLS
    };

    log { source(s_network_tls); destination(d_tls_logs); };

    $ sudo vim /var/ossec/etc/ossec.conf

    <localfile>
        <log_format>syslog</log_format>
        <location>/var/log/syslog-ng.log</location>
    </localfile>

    $ sudo systemctl enable syslog-ng
    $ sudo systemctl start syslog-ng