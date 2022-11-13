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


