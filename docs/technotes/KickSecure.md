Kick Secure Install:
--------------------

```
# Exisiting Debian 12 instance
sudo apt update
sudo apt remove plymouth
sudo apt install -y console-data console-common kbd keyboard-configuration extrepo 
sudo extrepo enable kicksecure
sudo /usr/sbin/addgroup --system console
sudo /usr/sbin/adduser $USER console
sudo apt update && sudo apt full-upgrade -y
sudo apt install -y kicksecure-xfce-host security-misc
sudo repository-dist --enable --repository stable
# Want the security , not tor? You can disable tor.
sudo systemctl disable tor
sudo systemctl stop tor
echo -e "[persistent-users]\nUser=$USER" | sudo tee /etc/privleap/conf.d/$USER.conf && sudo leapctl --reload && sudo leapctl --create $USER
sudo dpkg-reconfigure security-misc
# reboot
# Please test kick Secure before adding to production.
```

References:
----------
* https://www.kicksecure.com/wiki/Debian