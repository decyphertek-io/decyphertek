Linux-101
=====

Linux is an open source operating system. Learn how to navigate the terminal and do some basic tasks. 

Add user
--------

     # This will add a user to the following locations: /etc/passwd, /etc/shadow, /etc/group and /etc/gshadow
     # The -m option after useradd, will make a home directory.
     $ sudo useradd -m username
     $ sudo passwd username
     # Add to sudo group
     $ sudo usermod -aG sudo username
     # No sudo password for username
     $ sudo visudo
     username ALL=(ALL) NOPASSWD:ALL
     # Fix bash shell not showing username and hostname
     $ sudo chsh -s /bin/bash username

Remove a user
-------------

     # Make sure user is logged out
     $ sudo pkill -KILL -u username
     $ sudo deluser username
     # Manually remove from sudo no password
     $ sudo visudo
     # Delete and save
     username ALL=(ALL) NOPASSWD:ALL

Change Hostname

     $ sudo hostnamectl set-hostname "decyphertek"
     $ sudo su -c "echo '127.0.1.1 decyphertek' >> /etc/hosts"
     $ hostnamectl
     # Logout 

History
-------

     # Manually Change History
     $ vim ~/.bash_history
     # add your doc commands, so you dont have to type them
     $ exit
     # log back in
     $ history

System Info
-----------

     $ sudo apt install -y lsb-core
     $ lsb_release -a

Network Info
-------------

     # Get your ip address
     $ sudo apt install net-tools
     $ ifconfig
     # See listening ports 
     $ netstat -tuna

ACL
----

     $ sudo apt-get install nfs4-acl-tools acl
     # Read , Write , & Execute access to a single user
     $ setfacl -m u:username:rwx folder/
     # Read , Write , & Execute access to All Users in a group
     $ setfacl -m g:groupname:rwx folder/
     # You can set which permisisons you want the user or group to have.
     $ getfacl folder/
     # Revoke user access
     $ setfacl -x u:username,g:groupname folder/
     # Revoke group access
  

Enable AWS Workspace
--------------------

     # To enable access for your Linux system, please follow these steps :
     1. AWS Console > WorkSpaces > Directories 
     2. Your directory > Actions > Update Details
     3. Access Control Options > Check-Linux- platform > Update and Exit to save 
     

References
----------

https://linuxize.com/post/how-to-create-users-in-linux-using-the-useradd-command/
https://www.systutorials.com/docs/linux/man/8-deluser/
https://www.cyberciti.biz/faq/linux-logout-user-howto/
https://askubuntu.com/questions/388440/why-is-there-no-name-showing-at-the-command-line
https://www.howtogeek.com/197934/how-to-change-your-hostname-computer-name-on-ubuntu-linux/
https://linoxide.com/linux-set-access-control-list-using-setfacl-and-getfacl-commands/
https://linuxhint.com/change-hostname-ubuntu-permanently/

