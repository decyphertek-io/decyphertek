Falco
======

An open source docker security platform

Install & Use Falco:
--------------------

    # Install the keys
    curl -fsSL https://falco.org/repo/falcosecurity-packages.asc | \
    sudo gpg --dearmor -o /usr/share/keyrings/falco-archive-keyring.gpg

    # Add The Repo
    sudo bash -c 'cat << EOF > /etc/apt/sources.list.d/falcosecurity.list
    deb [signed-by=/usr/share/keyrings/falco-archive-keyring.gpg] https://download.falco.org/packages/deb stable main
    EOF'

    # Update & Install
    sudo apt update && sudo apt-get install -y dkms make linux-headers-$(uname -r) dialog falco
    # Select kmod & yes

    # Enable & Start Falco
    sudo systemctl enable falco
    sudo systemctl start falco
    sudo systemctl status falco

    # Enable a password rule
    sudo cat /etc/shadow > /dev/null

    # Check warning/sensitive alerts
    sudo journalctl _COMM=falco -p warning
    sudo grep Sensitive /var/log/syslog

References:
-----------

https://falco.org/docs/getting-started/falco-linux-quickstart/