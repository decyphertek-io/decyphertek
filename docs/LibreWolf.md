LibreWolf
=========

Secure fork of Firefox based on privacy. 

Install
-------

    # Change this command to choose a distro manually.
    $ distro=$(if echo " bullseye focal impish jammy uma una vanessa" | grep -q " $(lsb_release -sc) "; then echo $(lsb_release -sc); else echo focal; fi)
    $ wget -O- https://deb.librewolf.net/keyring.gpg | sudo gpg --dearmor -o /usr/share/keyrings/librewolf.gpg
    $ sudo tee /etc/apt/sources.list.d/librewolf.sources << EOF > /dev/null
      Types: deb
      URIs: https://deb.librewolf.net
      Suites: $distro
      Components: main
      Architectures: amd64
      Signed-By: /usr/share/keyrings/librewolf.gpg
      EOF
    $ sudo apt update
    $ sudo apt install librewolf -y

References
----------

    https://librewolf.net/
    https://librewolf.net/installation/debian/
