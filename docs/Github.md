Github
=====

     Github provides a cloud based git repo freely to those who open souece their code. Lets find an easy way to manage it. 

Add ssh keys
------------

     $ ssh-keygen -t ed25519 -C "email@domain"
     # select defaults with or without a passphrase.
     $ eval "$(ssh-agent -s)"
     $ ssh-add ~/.ssh/id_ed25519
     # Add the SSH key to your account on GitHub. 
     $ cat ~/.ssh/id_ed25519.pub
     1. Select and copy the contents of the id_ed25519.pub file
     2. In the upper-right corner of any page, click your profile photo, then click Settings. 
     3. In the "Access" section of the sidebar, click SSH and GPG keys.
     4. Click New SSH key or Add SSH key. 
     5. In the "Title" field, add a descriptive label for the new key. 
     6. Paste your key into the "Key" field. 
     7. Click Add SSH key. 
     8. If prompted, confirm access to your account on GitHub. For more information, see "Sudo mode."
     # Verify it Works
     $ ssh -T git@github.com

Setup
-----

     $ sudo apt install git 
     $ git config --global user.email "email@domain"
     $ git config --global user.name "username"
     $ cd  ~/git/
     # Need to run on each repo to commmit/push . 
     # If it is a private repo , need an access token OR ssh setup. 
     > Profile > Settings > Developer Settings > Personal Access Tokens > Generate New Token > Name it > Set Expiration > Select repos. 
     <OR>
     $ git clone git@github.com:account-name/repo-name.git --config core.sshCommand="ssh -i ~/.ssh/id_rsa"
     <OR>
     $ git clone https://github.com/acount-name/repo-name
     $ cd repo-name
     # Allow to push via ssh keys to cloned repo.
     $ git remote set-url origin git@github.com:account-name/repo-name.git
     # Make changes and commit. 
     $ git add .
     $ git commit -m "comment"
     $ git push

IDE Version Control
--------------------

     $ sudo snap install codium --classic
     # Open or git clone your repo
     # Add folder to workspace
     # Commit and push changes 


References
-----------

https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account
https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/sudo-mode
https://medium.com/@michael.rhema/how-to-use-specific-ssh-keys-for-git-push-4ecf3b31eeb4
https://gist.github.com/xirixiz/b6b0c6f4917ce17a90e00f9b60566278