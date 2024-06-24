Authelia
========

"Authelia is a 2FA & SSO authentication server which is dedicated to the security of applications and users. It can be considered an extension of reverse proxies by providing features specific to authentication."

Install
-------

    curl https://apt.authelia.com/organization/signing.asc | sudo apt-key add -
    sudo apt install -y apt-transport-https --yes
    echo "deb https://apt.authelia.com/stable/debian/debian/ all main" | sudo tee /etc/apt/sources.list.d/authelia-stable-debian.list
    sudo apt update && sudo apt -y install authelia=4.37.4-1
    # Need to configure the system or it will not load properly
    # Example errors
    level=error msg="Configuration: authentication_backend: you must ensure either the 'file' or 'ldap'>
    level=error msg="Configuration: access control: 'default_policy' option 'deny' is invalid: when no >
    level=error msg="Configuration: storage: configuration for a 'local', 'mysql' or 'postgres' databas>
    level=error msg="Configuration: storage: option 'encryption_key' is required"
    level=error msg="Configuration: notifier: you must ensure either the 'smtp' or 'filesystem' notifie>
    level=fatal msg="Can't continue due to the errors loading the configuration"
    # Work in progress, please reference the docs to complete the configs. 
    # Getting Started - https://www.authelia.com/integration/prologue/get-started/
    # Authelia Configuration Template - https://github.com/authelia/authelia/blob/master/config.template.yml
    # Authelia Config Example - https://gist.github.com/userdocs/7634b8a57e803e378b09c18225edd446
    sudo systemctl enable authelia
    sudo systemctl start authelia
    sudo systemctl status authelia

References
----------

    https://www.authelia.com/
    https://apt.authelia.com/stable/debian/packages/authelia/
    https://www.authelia.com/integration/prologue/get-started/
    https://www.authelia.com/integration/proxies/nginx/
    https://github.com/authelia/authelia