Kick Secure Install:
--------------------
```
# Exisiting Debian 12 instance
sudo apt update
sudo apt install extrepo 
sudo extrepo enable kicksecure
sudo /usr/sbin/adduser $USER console
sudo apt update && sudo apt full-upgrade 
sudo apt install --no-install-recommends kicksecure-xfce-host security-misc
```

References:
----------
* https://www.kicksecure.com/wiki/Debian