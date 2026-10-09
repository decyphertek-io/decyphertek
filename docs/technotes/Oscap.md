Oscap
=====

Oscap is the cli scanner from the OpenSCAP project. It uses the Security Content Automation
Protocol ( SCAP ) to audit & harden Linux servers against security benchmarks such as CIS,
DISA STIG, & ANSSI.

Caution
----------
* A scan without --remediate only reports what fails - it does not change the system.
* !!!CAUTION!!! - --remediate changes system settings & may break your system. Please practice on a test server, not production.
* Make sure you have a password set for sudo before you remediate. Most profiles enforce password authentication for sudo.
* Hardening has locked me out of systems in the past: passwd, adduser, & deluser can break, USB access can be blocked & some rules can lock you out entirely. Keep console access handy ( AWS instance screenshot, Azure boot troubleshooting, GCP serial console ) & test on a snapshot first.

Install - Scanner
----------
```
# Package name varies by distro release - use whichever one your distro has
sudo apt install -y openscap-scanner curl unzip 
OR
sudo apt install -y libopenscap8 curl unzip

# Verify
oscap --version
```

Install - Content ( Option 1: Distro Packages )
----------
```
# Newer releases ship SSG content packages - older releases use option 2
sudo apt install -y scap-security-guide 
OR
sudo apt install -y 'ssg-*'
```
* Data streams install to: /usr/share/xml/scap/ssg/content/
* If neither package exists for your release, use option 2.

Install - Content ( Option 2: Upstream Releases )
----------
Always the latest content & supports every OS version.
```
# Grab the latest release version
SSG_VERSION=$(curl -s https://api.github.com/repos/ComplianceAsCode/content/releases/latest | grep -oP '"tag_name":\s*"v\K[0-9.]+')

# Download & unzip
wget https://github.com/ComplianceAsCode/content/releases/download/v${SSG_VERSION}/scap-security-guide-${SSG_VERSION}.zip
unzip -q scap-security-guide-${SSG_VERSION}.zip
```

Data Streams
----------
Content ships one data stream per OS version. List the available data streams & point a variable at the one that matches your OS - it is reused for every command below:
```
# Option 1 - list installed data streams:
ls /usr/share/xml/scap/ssg/content/*-ds.xml

# Option 2 - list data streams from the unzipped release:
ls scap-security-guide-${SSG_VERSION}/*-ds.xml

# Point DS at the one that matches your OS:
DS=/path/to/ssg-YOUR-OS-ds.xml
```

Profiles
----------
List the profiles in your data stream:
```
oscap info $DS
```
Look for the Profile IDs, for example:
```
Profile ID: xccdf_org.ssgproject.content_profile_cis_level1_server
Profile ID: xccdf_org.ssgproject.content_profile_cis_level2_server
Profile ID: xccdf_org.ssgproject.content_profile_standard
Profile ID: xccdf_org.ssgproject.content_profile_stig
```
* Start with a lower level profile ( cis_level1 or standard ) first. Level 2 & STIG go much further.

Scan & Report
----------
```
mkdir ~/oscap-reports
sudo oscap xccdf eval \
  --profile xccdf_org.ssgproject.content_profile_standard \
  --results ~/oscap-reports/results.xml \
  --report ~/oscap-reports/report.html \
  $DS
```
* This only audits the server - nothing is changed.
* Copy the report off the server & open it in a browser:
```
scp user@server:~/oscap-reports/report.html .
```

Remediate
----------
!!!CAUTION!!! - Same scan as above, plus --remediate changes the system to try to fix what failed.
```
sudo oscap xccdf eval --remediate \
  --profile xccdf_org.ssgproject.content_profile_cis_level1_server \
  --results ~/oscap-reports/results.xml \
  --report ~/oscap-reports/report.html \
  $DS
```
* Re-run the scan without --remediate afterwards to confirm your score improved.
* If sudo, ssh or login breaks, use your console access to revert: restore a snapshot or comment out the pam changes in /etc/pam.d/common-password.

References
----------
* https://www.open-scap.org/
* https://github.com/ComplianceAsCode/content
* https://github.com/ComplianceAsCode/content/releases/latest
