Nmap
=====

Nmap is widely used by network administrators, security professionals, and ethical hackers to scan networks, identify open ports, detect running services and their versions, and determine the operating system of hosts within a network.

Nmap Debian Install
-------------------

      # To get the newest version of nmap on Debian based systems
      1. Download the Nmap RPMs for your platform (x86 or x86-64) from https://nmap.org/download.html
      2. sudo apt install alien
      3. sudo alien nmap-5.21-1.x86_64.rpm
      4. sudo dpkg --install nmap_5.21-2_amd64.deb
      # Steps 2–5 can be repeated for the other Nmap RPMs such as Zenmap, Ncat, and Nping.

Nmap Commands
-------------

     # Download the newest version. nmap -V
     https://nmap.org/download.html

     # Basic scan & multiple networks:
     $ sudo nmap 192.168.0.0/24 10.10.10.0/24

     # Quick scan no port check New 
     $ sudo nmap -sn 192.168.0.0/24

     # Scan for specific open ports
     $ sudo nmap -p 22,443 192.168.0.0/24

     # Scan for OS
     $ sudo nmap -O 192.168.0.0/24

     # OS and service Info
     $ sudo nmap -A 192.168.0.0/24

     # Identify Hostnames
     $ sudo nmap -sL 192.168.0.0/24

     # Agressive Quick Scan
     $ sudo nmap -T5 192.168.0.0/24

     # Perform a stealth scan:
     $ sudo nmap -sS 192.168.0.0/24

     # Output to xml
     $ sudo nmap -oX results.xml 192.168.0.0/24
     # XML output can be converted to HTML, easily parsed by programs such as Nmap graphical user interfaces, or imported into databases.
     # Can import xml to zenmap , scan, then view topology. 

Nmap Scripting Engine (NSE) (LUA)
---------------------------------

     NSE Scripts - https://github.com/topics/nmap-scripts?l=lua
     Roll your own NSE - https://null-byte.wonderhowto.com/how-to/get-started-writing-your-own-nse-scripts-for-nmap-0187403/
     https://www.tecmint.com/use-nmap-script-engine-nse-scripts-in-linux/
     https://nmap.org/book/nse.html
     https://nmap.org/presentations/BHDC10/

Nmap Troubleshooting
--------------------

     # Time Reduction of scans - solutions. 
     * Skip the port scan (-sn) 
     * Limit the number of ports scanned. --top-ports
     * Skip advanced scan types (-sC, -sV, -O, --traceroute, and -A)
     * Remember to turn off DNS resolution when it isn't necessary.  --system-dns 
     * Optimize Timing Parameters. -T
     * Separate and Optimize UDP Scans. -sSU
     * Upgrade Nmap. nmap -V
     * Execute Concurrent Nmap Instances. nmap-services and nmap-os-db
     https://nmap.org/book/reduce-scantime.html

     # OS misidentification - solutions
     * Upgrade to the latest Nmap
     * Scan all ports
     * Try a more aggressive guess
     * Scan from a different location
     # Submit Nmap OS DB fix. ( Excluding JUST GUESSING results)
     # verify output against similar systems.
     $ sudo nmap -O -sV -T4 -d <target>
     # Submit results here - https://insecure.org/cgi-bin/submit.cgi?corr-os
     https://nmap.org/book/osdetect-unidentified.html


Networking Models
-----------------

     OSI Model :
     7. Application
     6. Presentation
     5. Session
     4. Transport
     3. Network
     2. data link
     1. Physical 

     TCP/IP Model:
     1. Application layer
     2. Transport layer
     3. Network access layer
     4. Network interface layer
     5. Hardware layer

Network Mapping Alternatives
----------------------------

     * Zenmap ( Nmap GUI ) - https://www.redhat.com/sysadmin/quick-nmap-inventory
     * Spice Works - https://www.spiceworks.com/free-pc-network-inventory-software/
     * Cacti ( Server ) https://www.cacti.net/info/downloads ; https://www.howtoforge.com/how-to-install-cacti-monitoring-on-ubuntu-22-04/
     * Zmap - https://zmap.io/
     * Angry Ip Scanner - https://angryip.org/

References
-----------

     https://nmap.org/book/output-formats-commandline-flags.html
     https://www.redhat.com/sysadmin/quick-nmap-inventory
     https://www.secureideas.com/blog/2021/01/converting-nmap-xml-files-to-html-with-xsltproc.html
