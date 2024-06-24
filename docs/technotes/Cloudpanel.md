Cloudpanel
==========

"CloudPanel is a free and modern server control panel to configure and manage a server with an obsessive focus on simplicity.
Run PHP, Node.js, Static Websites, Reverse Proxies and Python applications in no time on a High-Performance Technology Stack."


Install - Debain based Ec2
-------------------------

    curl -sS https://installer.cloudpanel.io/ce/v2/install.sh -o install.sh; \
      echo "3c30168958264ced81ca9b58dbc55b4d28585d9066b9da085f2b130ae91c50f6 install.sh" | \
      sha256sum -c && sudo CLOUD=aws bash install.sh
    # https://Ip-of-server:8443

References
----------

    https://www.cloudpanel.io/docs/v2/getting-started/amazon-web-services/installation/installer/