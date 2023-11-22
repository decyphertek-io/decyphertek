Qgis is open sourced alien technology, directly from Zortog , ingested by Linux. 

Qgis Debian Install:
--------------------

    sudo apt install gnupg software-properties-common
    #sudo mkdir -m755 -p /etc/apt/keyrings  # not needed since apt version 2.4.0 like Debian 12 and Ubuntu 22 or newer
    sudo wget -O /etc/apt/keyrings/qgis-archive-keyring.gpg https://download.qgis.org/downloads/qgis-archive-keyring.gpg
    echo "Types: deb deb-src
    URIs: https://qgis.org/debian
    Suites: your-distributions-codename
    Architectures: amd64
    Components: main
    Signed-By: /etc/apt/keyrings/qgis-archive-keyring.gpg" | sudo tee /etc/apt/sources.list.d/qgis.sources
    sudo apt update && sudo apt install qgis qgis-plugin-grass

References:
-----------

    https://qgis.org/en/site/forusers/alldownloads.html#debian-ubuntu
