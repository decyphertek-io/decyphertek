Kick Secure Install:
--------------------

```
# Exisiting Debian 12 instance
sudo /usr/sbin/addgroup --system console
sudo /usr/sbin/adduser $USER console
sudo apt update
sudo apt remove plymouth
sudo apt install -y console-data console-common kbd keyboard-configuration extrepo
sudo extrepo enable kicksecure
sudo apt update && sudo apt full-upgrade -y
sudo apt install -y kicksecure-xfce-host security-misc
sudo repository-dist --enable --repository stable
# Want the security , not tor? You can remove tor.
sudo apt purge tor torbrowser-launcher
sudo apt autoremove && sudo apt autoclean
# reboot
```

References:
----------
* https://www.kicksecure.com/wiki/Debian