Windows
--------

Install a package manager and some basic security applications. 

Chocolately Install
-------------------

    # Open Powershell as administrator > right click.
    > Set-ExecutionPolicy AllSigned
    > Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
    # Install Choco GUI
    > choco install chocolateygui
    # Search Packages
    > choco search PackageName 
    # Install Packages
    > choco install PackageName
    # Uninstall Packages
    > choco uninstall PackageName
    # Upgrade Packages
    > choco upgrade PackageName
    # Upgrade all Packages
    > choco upgrade all

Chocolately Recommened Packages
-------------------------------

    # Secure Firefox Fork
    > Choco install librewolf
    # Windows Privacy
    > choco install blackbird
    # SandBox Applications
    > choco install sandboxie
    # Authy Desktop
    > choco install authy-desktop
    # Remote Access
    > choco install mobaxterm
    # Free FTP
    > choco install filezilla
    # AntiVirus Option 1
    > choco install immunet
    # AntiVirus Option 2
    > choco install f-secureav
    # Password Manager
    > choco install bitwarden
    # DB Editor and Manager
    > choco install dbeaver
    # WebSite Scanner Option #1
    > choco install burp-suite-free-edition
    # WebSite Scanner Option #2
    > choco install zap
    # Malware Reverse Engineering
    > choco install ghidra
    # Privacy Cleaner
    > choco install bleachbit
    # Modern VPN
    > choco install wireguard
    # Network Scanner
    > choco install nmap
    # Explore AD
    > choco install adexplorer
    # Hash Checker
    > choco install gtkhash
    # Encryption
    > choco install veracrypt   
    # Open Source VSCode
    > choco install vscodium
    # Backup Solution 
    > choco install duplicati
    # Burn USB & SD
    > choco install etcher
    # Open Source Office Suite
    > choco install libreoffice-fresh
    # Media Player
    > choco install vlc
    # Music Player
    > choco install spotube

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
    https://medium.com/nerd-for-tech/upgrade-all-software-with-one-click-with-choco-and-total-commander-7752876f3f0d
    
