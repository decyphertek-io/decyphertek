Nmap
=====

Nmap is widely used by network administrators, security professionals, and ethical hackers to scan networks, identify open ports, detect running services and their versions, and determine the operating system of hosts within a network.

Nmap Install
-------------------

      # Nmap for all Operating Systems. - https://nmap.org/download.html
      # Best practice is to use the newest version of nmap, provides fixes.

      # The suggested debian method doesnt work well using alien. Use apt instead.
      $ sudo apt install nmap
      # Install zenmap 
      $ wget http://archive.ubuntu.com/ubuntu/pool/universe/n/nmap/zenmap_7.60-1ubuntu5_all.deb
      $ sudo dpkg -i zenmap_7.60-1ubuntu5_all.deb

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
     #  --webxml Makes it readable in web browser.
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

Nmap Timing 
-----------

     # Timing templates
     $ sudo nmap -T[0-5] [target]
	
     # Set the packet TTL
     $ sudo nmap --ttl [time] [target]
	
     # Setting the --min-parallelism option may increase scan performance, setting it too high may produce inaccurate results.
     # Minimum number of parallel operations
     $ sudo nmap --min-parallelism [number] [target]
	
     # Maximum number of parallel operations
     $ sudo nmap --max-parallelism [number] [target]

     # Minimum host group size	
     $ sudo nmap --min-hostgroup [number] [targets]

     # Maximum host group size	
     $ sudo nmap --max-hostgroup [number] [targets]

     # Maximum RTT timeout
     $ sudo nmap --initial-rtt-timeout [time] [target]

     # Initial RTT timeout
     $ sudo nmap --max-rtt-timeout [TTL] [target]
	
     # Maximum number of retries
     $ sudo nmap --max-retries [number] [target]
	
     # Host timeout
     $ sudo nmap --host-timeout [time] [target]
	
     # Minimum scan delay
     $ sudo nmap --scan-delay [time] [target]
	
     # Maximum scan delay
     $ sudo nmap --max-scan-delay [time] [target]
	
     # Minimum packet rate   
     $ sudo nmap --min-rate [number] [target]
	
     # Maximum packet rate
     $ sudo nmap --max-rate [number] [target]
	
     # Defeat reset rate limits 
     $ sudo nmap --defeat-rst-ratelimit [target]
	
Nmap NSE - Scripting Engine
---------------------------------

     # NSE Scripts - https://nmap.org/nsedoc/scripts/
     # Roll your own NSE - https://null-byte.wonderhowto.com/how-to/get-started-writing-your-own-nse-scripts-for-nmap-0187403/

     # Find script using locate
     $ locate *.nse
 
     # Execute individual scripts
     $ sudo nmap --script [script.nse] [target]
	
     # Execute multiple scripts
     $ sudo nmap --script [expression] [target]
	
     # Execute scripts by category
     $ sudo nmap --script [category] [target]
	
     # Execute multiple script categories
     $ sudo nmap --script [category1,category2,etc]
	
     # Troubleshoot scripts
     $ sudo nmap --script [script] --script-trace [target]
	
     # Update the script database 
     $ sudo nmap --script-updatedb

     # Example Script snmp-info - https://nmap.org/nsedoc/scripts/snmp-info.html
     $ sudo nmap --script snmp-info.nse [target]
	
Nmap Troubleshooting
--------------------

     # Time Reduction of scans - https://nmap.org/book/reduce-scantime.html
     * Skip the port scan (-sn) 
     * Limit the number of ports scanned. --top-ports
     * Skip advanced scan types (-sC, -sV, -O, --traceroute, and -A)
     * Remember to turn off DNS resolution when it isn't necessary.  --system-dns 
     * Optimize Timing Parameters. -T
     * Separate and Optimize UDP Scans. -sSU
     * Upgrade Nmap. nmap -V
     * Execute Concurrent Nmap Instances. nmap-services and nmap-os-db
     
     # OS misidentification - https://nmap.org/book/osdetect-unidentified.html
     * Upgrade to the latest Nmap
     * Scan all ports
     * Try a more aggressive guess
     * Scan from a different location
     # Submit Nmap OS DB fix. ( Excluding JUST GUESSING results)
     # verify output against similar systems.
     $ sudo nmap -O -sV -T4 -d <target>
     # Submit results here - https://insecure.org/cgi-bin/submit.cgi?corr-os
     
     # Getting help
     $ sudo nmap -h
	
     # Display nmap version
     $ sudo nmap -V

     # Verbose output	
     $ sudo nmap -v [target]
	
     # Debugging
     $ sudo nmap -d [target]
	
     # Display port state reason
     $ sudo nmap --reason [target]
	
     # Only display open ports
     $ sudo nmap --open [target]
	
     # Trace packets
     $ sudo nmap --packet-trace [target]
	
     # Display host networking
     $ sudo nmap --iflist
	
     # Specify a network interface
     $ sudo nmap -e [interface] [target]

Optional: Nmap Infosec 
----------------------
     
     # If you add scripts, update the DB
     $ sudo nmap --script-updatedb

     # Vulners scan
     $ sudo nmap -Pn -sV --script vulners [target]

     # Check SSL cert
     $ sudo nmap --script ssl-cert -p 443 -v [target]

     # Whois-domain
     $ sudo nmap --script whois-domain.nse [target]

     # 
    
     # Geolocation
     $ Wget http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz
     $ sudo mv GeoLiteCity.dat.gz /usr/local/share/nmap/nselib/data/GeoLiteCity.dat.gz
     $ sudo nmap --script ip-geolocation-* [target]

     # Google Safe Browsing
     # Get API Key - http://code.google.com/apis/safebrowsing/key_signup.html
     $ sudo nmap -p80 --script http-google-malware –script-args http-google-malware.api=<API> [target]

     # Email
     $ wget http://seclists.org/nmap-dev/2011/q3/att-401/http-google-email.nse 
     $ sudo mv http-google-email.nse  /usr/share/nmap/scripts/http-google-email.nse 
     $ sudo nmap -p80 --script http-google-email [target]

Optional: Ansible Nmap
------------------

     # https://docs.ansible.com/ansible/latest/collections/community/general/nmap_inventory.html
     # Requirement: Install ansible galaxy community general
     $ sudo ansible-galaxy collection install community.general
     # Reference community.general.nmap in the Ansible Playbook
     # inventory.config file in YAML format

     plugin: community.general.nmap
     strict: false
     address: 192.168.0.0/24

     # a sudo nmap scan to fully use nmap scan power.
     plugin: community.general.nmap
     sudo: true
     strict: false
     address: 192.168.0.0/24

     # an nmap scan specifying ports and classifying results to an inventory group
     plugin: community.general.nmap
     address: 192.168.0.0/24
     exclude: 192.168.0.1, web.example.com
     port: 22, 443
     groups: web_servers: "ports | selectattr('port', 'equalto', '443')"

Optional: Real World Scenarios
------------------------------

     # Scanning multiple large subnets 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16, confirm network access to those subnets. 
     # Scanning multiple large subnets can take a lot of try some of the mentioned solutions:
     #  --min-rate, --max-parallelism, and --host-timeout

     # Its faster to scan one subnet at a time, if you want to scan then all, then:
     $ sudo nmap -sn 10.0.0.0/8 , 192.168.0.0/16 , 172.16.0.0/12

     # Quick inventory, OS , Ports. 
     $ sudo vim nmap.sh
     sudo nmap -sn 192.168.0.0/24 | awk '/Nmap scan/{gsub(/[()]/,"",$NF); print $NF > "livehosts.txt"}'
     sudo nmap -O --osscan-limit -iL livehosts.txt -oX livehosts-OS.xml 
     xsltproc livehosts-OS.xml -o livehosts-OS.html
     $ bash nmap.sh
     # Read results in web browser or lynx . 

     # Consider masscan to scan large subnets, suppose to be faster, nmap was faster on 192.168.0.0/24 using -sn -Pn and masscan would kick me off my VPN. 
     $ sudo apt install masscan
     $ sudo masscan -p0-65535 --rate=50000 10.0.0.0/8,192.168.0.0/16,172.16.0.0/12 | awk '/Nmap scan/{gsub(/[()]/,"",$NF); print $NF > "livehosts.txt"}'
     # Then use nmap
     $ sudo nmap -O --osscan-limit -iL livehosts.txt -oX livehosts-OS.xml 
     $ xsltproc livehosts-OS.xml -o livehosts-OS.html

     # Get a second Opinion on namp OS results. 
     $ sudo xprobe2 192.168.0.1

     # Netdiscover can also map an unknown network easily
     $ sudo apt install netdiscover
     $ sudo netdiscover
     # Scan a specific subnet and save output
     $ sudo netdiscover -f -r 192.168.0.0/24 -PN | awk '{print $1}' > livehosts.txt
     # Can feed this to nmap.
     # I found that it didnt pick up my system? Maybe the firewall is blocking the probe?

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
     * Zmap ( Public Networks ) - https://zmap.io/
     * Angry Ip Scanner - https://angryip.org/
     * LibreNMS ( Server ) - https://www.librenms.org/
     * OpenNMS ( Server) - https://www.opennms.com/distributions/
     * Nagios ( Server ) https://www.nagios.org/projects/nagios-core/

References
-----------

     https://nmap.org/book/output-formats-commandline-flags.html
     https://www.redhat.com/sysadmin/quick-nmap-inventory
     https://duckduckgo.com/?t=ffab&q=nmap+cheat+sheet&ia=cheatsheet&iax=1
     https://www.tecmint.com/use-nmap-script-engine-nse-scripts-in-linux/
     https://nmap.org/book/nse.html
     https://nmap.org/presentations/BHDC10/
     https://docs.ansible.com/ansible/latest/collections/community/general/nmap_inventory.html
     https://www.secureideas.com/blog/2021/01/converting-nmap-xml-files-to-html-with-xsltproc.html
     https://resources.infosecinstitute.com/topic/nmap-cheat-sheet-discovery-exploits-part-3-gathering-additional-information-host-network-2/

