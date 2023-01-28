CIS / Oscap
=====

!!!CAUTION!!! - This may break your system. Please practice on test server, not production.
CIS - Center For Internet Security provides easy to use benchmarks to secure a system. OSCAP 
is the cli tool from OpenScap that utilizes the Open Security Automation Protocol to 
secure Linux servers. 

     # More options at: https://github.com/ComplianceAsCode/content/ 
     # Make sure that you have a password set, CIS3/oscap enforces the use of a password to use sudo. 
     # All CIS & Oscap break the passwd, adduser, and deluser commands. Breaks Usb Access. See the fix below ( No fix yet USB.) 
     # CIS Level 1 with the passwd pam fix, works the best.
     # CIS Level 2 breaks auditd, unresolved.
     # CIS Level 3 & Oscap, lock me out of the system and unable to use sudo, unresolved. 
  
CAUTION: CIS Level1 - Ubuntu 20.04 Server
-----------------------------------------

     $ curl -sSL https://raw.githubusercontent.com/decyphertek-io/configs/main/bash-scripts/ubuntu2004-script-cis_level1_server.sh | sudo bash

CAUTION: CIS Level2 - Ubuntu 20.04 Server
-----------------------------------------

     $ curl -sSL https://raw.githubusercontent.com/decyphertek-io/configs/main/bash-scripts/ubuntu2004-script-cis_level2_server.sh | sudo bash

CAUTION: CIS Level3/Stig V1R1 - Ubuntu 20.04 Server
---------------------------------------------------

     $ curl -sSL https://raw.githubusercontent.com/decyphertek-io/configs/main/bash-scripts/ubuntu2004-script-stig-cis_level3_server.sh | sudo bash

Oscap - Install
----------------

     $ sudo apt install -y libopenscap8 ssg-base ssg-debderived ssg-debian ssg-nondebian ssg-applications unzip
     $ wget https://github.com/ComplianceAsCode/content/releases/download/v0.1.63/scap-security-guide-0.1.63.zip 
     $ unzip -q scap-security-guide-0.1.63.zip
     $ sudo mkdir /opt/ssg/
     $ mkdir ~/ssg-reports/
     $ sudo mv scap-security-guide-0.1.63 /opt/ssg/
     $ sudo rm -rf scap-security-guide-0.1.63.zip
  
CAUTION: Oscap - Quick Remediation
----------------------------------

     $ sudo oscap xccdf eval --remediate --profile xccdf_org.ssgproject.content_profile_stig \
     /opt/ssg/scap-security-guide-0.1.63/ssg-ubuntu2004-ds.xml > ~/ssg-reports/ssg-ubuntu2004-ds.txt
     $ cat ~/ssg-reports/ssg-ubuntu2004-ds.txt

Optional
--------

     # All CIS & Oscap break the passwd, adduser, and deluser commands. The fix .
     $ sudo sed -i 's/password requisite pam_pwhistory\.so remember=5  use_authtok/#password requisite pam_pwhistory\.so remember=5  use_authtok/g' /etc/pam.d/common-password 
     $ sudo sed -i 's/password requisite pam_pwquality\.so retry=3/#password requisite pam_pwquality\.so retry=3/g' /etc/pam.d/common-password
  
  
References
----------

     https://www.open-scap.org/
     https://manpages.ubuntu.com/manpages/xenial/man8/oscap.8.html
     https://www.cisecurity.org/cis-benchmarks/cis-benchmarks-faq
     https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security_guide/sect-using_openscap_to_remediate_the_system
     https://askubuntu.com/questions/1390222/passwd-module-is-unknown
     https://adamtheautomator.com/openscap/


