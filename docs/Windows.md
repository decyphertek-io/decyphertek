Windows
--------

Secure windows and install a package manager.

Chocolately Install
-------------------

    # Open Powershell as administrator > right click.
    > Set-ExecutionPolicy AllSigned
    > Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
    # Search Packages
    > choco search pakagename 
    # Install example
    > choco install bleachbit

Firewall Install
----------------

    # SimpleWall - Download and install 
    https://github.com/henrypp/simplewall/releases/download/v.3.6.7/simplewall-3.6.7-setup.exe
    # Launch > Enable Filter > Allow/Deny applications as they pop up .

Crowdsec Install
-----------------
  
    # Download Crowdsec and install 
    https://github.com/crowdsecurity/crowdsec/releases/download/v1.4.1/crowdsec_1.4.1.msi
    # Install Windows Collection via Crowdsec
    > cscli collections install crowdsecurity/windows
    # install Crowdsec firewall bouncer
    > choco install crowdsec-windows-firewall-bouncer

References
----------

    https://chocolatey.org/install
    https://community.chocolatey.org/packages/
    https://www.henrypp.org/product/simplewall
    https://www.crowdsec.net/
    https://docs.crowdsec.net/docs/next/getting_started/install_windows/