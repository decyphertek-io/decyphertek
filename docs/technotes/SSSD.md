SSSD
=====

SSSD offers a way that Linux can connect to Active Directory. 

Install
-------

    $ sudo apt install sssd-ad sssd-tools realmd adcli
    $ sudo realm -v discover ad1.example.com
    $ sudo realm join -v ad1.example.com
    Password for Administrator: 
    $ sudo pam-auth-update --enable mkhomedir

Note
-----
    By default, realm will use the Administrator account of the domain to request the join. 
    If you need to use another account, pass it to the tool with the -U option.

    Another popular way of joining a domain is using an OTP, or One Time Password, token. 
    For that, use the --one-time-password option.

SSD.conf
--------

    $ sudo vim /etc/sssd/sssd.conf

    [sssd] 
    domains = ad1.example.com 
    config_file_version = 2 
    services = nss, pam 

    [domain/ad1.example.com] 
    default_shell = /bin/bash 
    krb5_store_password_if_offline = True 
    cache_credentials = True 
    krb5_realm = AD1.EXAMPLE.COM 
    realmd_tags = manages-system 
    joined-with-adcli id_provider = ad 
    fallback_homedir = /home/%u@%d 
    ad_domain = ad1.example.com 
    use_fully_qualified_names = True 
    ldap_id_mapping = True 
    access_provider = ad

Checks
------

    $ getent passwd john@ad1.example.com
    $ groups john@ad1.example.com

Login
-----

    $ ssh john@ad1.example.com@10.51.0.11


References
----------

    https://ubuntu.com/server/docs/service-sssd-ad