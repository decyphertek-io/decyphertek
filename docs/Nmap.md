Nmap
=====

Nmap is widely used by network administrators, security professionals, and ethical hackers to scan networks, identify open ports, detect running services and their versions, and determine the operating system of hosts within a network.

Nmap Install
-------------------

      # Nmap for all Operating Systems. - https://nmap.org/download.html
      Best practice is to use the newest version of nmap. The newest version can solves previous issues
      regarding OS mapping accuracy and other glitches. 

      # To get the newest version of nmap on Debian based systems ( apt repo doesnt have newest version )
      # Download the Nmap RPMs for your platform (x86 or x86-64) from https://nmap.org/download.html
      $ sudo apt install alien
      $ sudo alien nmap-5.21-1.x86_64.rpm
      $ sudo dpkg --install nmap_5.21-2_amd64.deb
      # Can also be used to install other Nmap RPMs such as Zenmap, Ncat, and Nping.

Nmap Basics
-------------

     # replace all [name] with a variable without brackets. 
     # EX: Replace [target] with IP or CIDR range. 192.168.0.1 or 192.168.0.0/24 . 
     # You can find the subnet from a system on the network. $ ifconfig OR $ ip addr

     # Scan a single target
     $ sudo nmap [target]
     
     # Scan multiple targets
     $ sudo nmap [target1], [target2], [target3]

     # Scan a list of targets
     $ nmap -iL [list.txt]

     # Scan an entire subnet
     $ sudo nmap [target]

     # Scan random hosts
     $ sudo nmap -iR [number]

     # Excluding targets from a scan
     $ sudo nmap [target] --exclude [target1]

     # Excluding targets using a list
     $ sudo nmap [target] --excludefile [list.txt]

     # Perform an agressive scan
     $ sudo nmap -A [target]

     # Scan an IPv6 target
     $ sudo nmap -6 [target]

Nmap Discovery 
--------------

     # Perform a ping-only scan
     $ sudo nmap -sn [target]
	
     # Don't ping
     $ sudo nmap -Pn [target]
	
     # TCP SYN ping
     $ sudo nmap -PS [target]
	
     # TCP ACK ping
     $ sudo nmap -PA [target]
	
     # UDP ping
     $ sudo nmap -PU [target]
	
     # SCTP INIT ping
     $ sudo nmap -PY [target]
	
     # ICMP echo ping
     $ sudo nmap -PE [target]
	
     # ICMP timestamp ping
     $ sudo nmap -PP [target]
	
     # ICMP address mask ping
     $ sudo nmap -PM [target]
	
     # IP protocol ping
     $ sudo nmap -PO [target]
	
     # ARP ping
     $ sudo nmap -PR [target]
	
     # Traceroute
     $ sudo nmap --traceroute [target]
	
     # Force reverse DNS resolution
     $ sudo nmap -R [target]
	
     # Disable reverse DNS resolution
     $ sudo nmap -n [target]
	
     $ Alternative DNS lookup
     $ sudo nmap --system-dns [target]
	
     # Manually specify DNS server(s)
     $ nmap --dns-servers [servers] [target]
	
     # Create a host list 
     $ sudo nmap -sL [targets]

Nmap Port Scanning
------------------

     # Perform a fast scan
     $ sudo nmap -F [target]
	
     # Scan specific ports
     $ sudo nmap -p [port(s)] [target]
	
     # Scan ports by name
     $ sudo nmap -p [port name(s)] [target]
	
     # Scan ports by protocol
     $ sudo nmap -sU -sT -p U:[ports],T:[ports] [target]
	
     # Scan all ports
     $ sudo nmap -p 1-65535 [target]
	
     # Scan top ports
     $ sudo nmap --top-ports [number] [target]
	
     # Perform a sequential port scan
     $ sudo nmap -r [target]
	
     # Attempt to guess an unknown OS
     $ sudo nmap -O --osscan-guess [target]
	
     # Service version detection
     $ sudo nmap -sV [target]
	
     # Troubleshooting version scans
     $ sudo nmap -sV --version-trace [target]
	
     # Perform a RPC scan
     $ sudo nmap -sR [target]

Nmap Advanced Scans
-------------------

     # TCP SYN scan
     $ sudo nmap -sS [target]
	
     # TCP connect scan
     $ sudo nmap -sT [target]
	
     # UDP scan
     $ sudo nmap -sU [target]
	
     # TCP NULL scan
     $ sudo nmap -sN [target]
	
     # TCP FIN scan
     $ sudo nmap -sF [target]
	
     # Xmas scan
     $ sudo nmap -sA [target]
	
     # TCP ACK scan
     $ sudo nmap -sA [target]
	
     # Custom TCP scan
     $ sudo nmap --scanflags [flags] [target]
	
     # IP protocol scan
     $ sudo nmap -sO [target]
	
     # Send raw ethernet packets
     $ sudo nmap --send-eth [target]
	
     # Send IP packets 
     $ sudo nmap --send-ip [target]

Nmap Firewall Evasion 
---------------------

     # Fragment packets
     $ sudo nmap -f [target]
	
     # Specify a specific MTU
     $ sudo nmap --mtu [MTU] [target]
	
     # Use a decoy
     $ sudo nmap -D RND:[number] [target]
	
     # Idle zombie scan
     $ sudo nmap -sI [zombie] [target]
	
     # Manually specify a source port
     $ sudo nmap --source-port [port] [target]
	
     # Append random data
     $ sudo nmap --data-length [size] [target]
	
     # Randomize target scan order
     $ sudo nmap --randomize-hosts [target]
	
     # Spoof MAC address
     $ sudo nmap --spoof-mac [MAC|0|vendor] [target]
	
     # Send bad checksums 
     $ sudo nmap --badsum [target]

Nmap Output
------------

     # Save output to a text file
     $ sudo nmap -oN [scan.txt] [target]
	
     # Save output to a XML file
     $ sudo nmap -oX [scan.xml] [target]
	
     # Grepable output
     $ sudo nmap -oG [scan.txt] [target]
	
     # Output all supported file types
     $ sudo nmap -oA [path/filename] [target]
	
     # Periodically display statistics
     $ sudo nmap --stats-every [time] [target]
	
     # 333 output 
     $ sudo nmap -oS [scan.txt] [target]

Ndiff nmap scans
----------

     # Install ndiff on debian sysyems
     $ sudo apt install ndiff

     # Comparison using Ndiff
     $ sudo ndiff [scan1.xml] [scan2.xml]

     # Ndiff verbose mode	
     $ sudo ndiff -v [scan1.xml] [scan2.xml]
	
     # XML output mode 
     $ sudo ndiff --xml [scan1.xml] [scan2.xml]
	
Nmap Scripting Engine (NSE) (LUA)
---------------------------------

     NSE Scripts - https://nmap.org/nsedoc/scripts/
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
     https://duckduckgo.com/?t=ffab&q=nmap+cheat+sheet&ia=cheatsheet&iax=1
     https://www.secureideas.com/blog/2021/01/converting-nmap-xml-files-to-html-with-xsltproc.html
     https://resources.infosecinstitute.com/topic/nmap-cheat-sheet-discovery-exploits-part-3-gathering-additional-information-host-network-2/

