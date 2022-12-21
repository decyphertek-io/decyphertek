Authelia
========

Open Source Web Auth , Way better than Keycloak. This is awesome. Can add as a security feature, to secure those servers that do not comply with AWS. 

Install
-------

    $ curl https://apt.authelia.com/organization/signing.asc | sudo apt-key add -
    $ sudo apt-get install -y apt-transport-https --yes
    $ echo "deb https://apt.authelia.com/stable/debian/debian/ all main" | sudo tee /etc/apt/sources.list.d/authelia-stable-debian.list
    $ sudo apt-get update && sudo apt-get install authelia=4.37.4-1
    # Need to configure the system or it will not load properly
    # Example errors
    Dec 21 08:15:19 decyphertek authelia[33039]: time="2022-12-21T08:15:19Z" level=error msg="Configuration: authentication_backend: you must ensure either the 'file' or 'ldap'>
    Dec 21 08:15:19 decyphertek authelia[33039]: time="2022-12-21T08:15:19Z" level=error msg="Configuration: access control: 'default_policy' option 'deny' is invalid: when no >
    Dec 21 08:15:19 decyphertek authelia[33039]: time="2022-12-21T08:15:19Z" level=error msg="Configuration: storage: configuration for a 'local', 'mysql' or 'postgres' databas>
    Dec 21 08:15:19 decyphertek authelia[33039]: time="2022-12-21T08:15:19Z" level=error msg="Configuration: storage: option 'encryption_key' is required"
    Dec 21 08:15:19 decyphertek authelia[33039]: time="2022-12-21T08:15:19Z" level=error msg="Configuration: notifier: you must ensure either the 'smtp' or 'filesystem' notifie>
    Dec 21 08:15:19 decyphertek authelia[33039]: time="2022-12-21T08:15:19Z" level=fatal msg="Can't continue due to the errors loading the configuration"
    # Work in progress, please reference the docs to complete the configs. 
    # Getting Started - https://www.authelia.com/integration/prologue/get-started/
    $ sudo systemctl enable authelia
    $ sudo systemctl start authelia
    $ sudo systemctl status authelia

References
----------

    https://www.authelia.com/
    https://apt.authelia.com/stable/debian/packages/authelia/
    https://www.authelia.com/integration/prologue/get-started/
    https://www.authelia.com/integration/proxies/nginx/
    https://github.com/authelia/authelia