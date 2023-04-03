Nmap
=====

Nmap is widely used by network administrators, security professionals, and ethical hackers to scan networks, identify open ports, detect running services and their versions, and determine the operating system of hosts within a network.

Nmap Commands
-------------

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

     # Additional Functionality -  Scripting engine.
     https://www.tecmint.com/use-nmap-script-engine-nse-scripts-in-linux/
     https://nmap.org/book/nse.html
     https://nmap.org/presentations/BHDC10/

     # Time Reduction of scans
     https://nmap.org/book/reduce-scantime.html

     # OS misidentification
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

References
-----------

     https://nmap.org/book/output-formats-commandline-flags.html
     https://www.redhat.com/sysadmin/quick-nmap-inventory
     https://www.secureideas.com/blog/2021/01/converting-nmap-xml-files-to-html-with-xsltproc.html