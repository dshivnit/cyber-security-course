Tools mainly being used so far in this course will be described here (note - there are HEAPS out there - refer to the Book of "Secret" Knowledge - lel, secret)
*Perhaps put these into their own sections and further expand.
ie Windows applications/software, Other OS applications/software, PowerShell tools, Unix/Linux shell tools - differentiating between the different shells if relevant (bash, zsh etc) - atm this section is all jumbled up*

- Everything
	- Pretty neat, kind of like Finder in MacOS, real fast to search for stuff when compared to your usual File Explorer in Windows
	- voidtools.com
	- Quick filename indexing
- Burp Suite
	- Software security application used for penetration testing of web applications
	- Well-known use cases involve scanning for many types of vulnerabilities.
	- Can identify common security flaws such as SQL injection, XSS (Cross-site Scripting), CSRF (Cross-site Request Forgery), and more..
	- https://portswigger.net/burp
- Nessus
	- Made by Tenable
	- A proprietary vulnerability scanner
	- Alternative to Burp Suite
	
- PuTTY - Pretty Useful Teletypewriter
	- Good way to telnet, SSH so on so forth to machines
	  https://www.putty.org/
- Have I Been Pwned?
	  https://haveibeenpwned.com/
- nmap
	- NSE - NMap Scripting Engine
		- Written in the Lua programming language
			- Scanning for vulns
			- Automating exploits
			- Recon
			- Categories:
				- safe - won't affect the target
				- intrusive - not safe, most likely will affect the target
				- vuln - probing for vulns
				- exploit - attempt to exp a vuln
				- auth - attempt to bypass authentication for running services (like FTP)
				- brute - attempt to bf creds for running services
				- discovery - query running services for further info on the network
		- --script=< script_name > (can use commas to run multiple scripts at za same time)
		- /usr/share/nmap/scripts
			- alluvdem
			- script.db (for details of the list)
	- ping sweep
		- nmap will send an ICMP packet to each possible IP address in the given network
			- It will mark valid responses as active hosts
			- Forms somewhat of a baseline
			- (do you want to accept ICMP or not?)
				- -sn ip_netaddr.+1-254 for example
	- **-p- asks Nmap to scan every possible TCP port**, -v asks Nmap to be verbose about it, -A enables aggressive tests such as remote OS detection, service/version detection, and the Nmap Scripting Engine (NSE). Finally, -T4 enables a more aggressive timing policy to speed up the scan. (nmap.org)
	- https://www.stationx.net/nmap-cheat-sheet/
	- -open : Only show open (or possibly open) ports
	- example: nmap -open -p- -T5 *ip_address/hostname*
		- This will scan for all open ports
		- Scanning all ports up to 65535 (max number of possible ports)
		- Trying to go as fast as it can
	- -sV : Probe open ports to determine service/version info
	- -sC : equivalent to --script=default
	- -p- : scan all ports
	- -sT
		- TCP Connect Scans
	- -sS
		- SYN "Half-open" scans, or "stealth" scans
		- Second packet sent is an RST to stop the other side from repeatedly trying to get an ACK back (this is after getting a SYN/ACK from it)
		- Some services are bought down by SYN scans
			- Keep this in mind if the client (or scenario) involves a Prod Env
		- Can be issued with CAP_NET_RAW, CAP_NET_ADMIN, CAP_NET_BIND_SERVICE
			- keep note that this may bugger some of the NSE scripts to run
		- SYN scans do not form the whole three-way handshake, 'member that
			- Hence why they're considered half-open and stealthy, as most detection systems will only pick up active connections, wherein a handshake has been completed
				- *This to be contested with further research down the line and testing*
	- -sU
		- UDP Scans
		- UDP ports don't respond. (response given by end-node is "open|filtered")
			- Closed is closed (unreachable)
			- Responses given with ICMP
		- Consider, top 20 ports being UDP scanned (system design to revert commonly used ports and so on)
		- UDP scans with NMAP take a long, long time. 
	- -sN
		- TCP Null Scans
		- No flag packet sent
	- -sF
		- TCP FIN Scans
		- FIN flag packet sent
	- -sX
		- TCP Xmas Scans
		- A radiated mungbean packet is sent
				The last three above will expect a 'open|filtered' 'closed' or 'filtered' response
				if a filtered response is given, the other side sent an ICMP packet
				RFC 793 states that hosts respond to malformed (radiated mungbean ;) ) packets with a RST TCP packet for ports that are closed
					No response at all for open ports.
				Consider:
					Most firewalls drop TCP packets to blocked ports which have the SYN flag set.
						Sending packets which aren't with a SYN flag steps through this (depends on *design* and config)
					Windows and Cisco devices respond with an RST packet to a radiated mungbean incoming packet
						Which describes a closed port, when in actuality it is open.
	- -Pn
		- Don't send an ICMP / ping packet before scanning 
		- nmap will treat the host as being alive
			- bypasses ICMP blocks
			- Takes a flapping long time (even if the host truly is offline, or not there)
				consider: ARP
	- -f
		- Fragment packets
	- --mtu (maximum transmittable unit) < number >
		- (has to be a multiple of 8)
	- --scan-delay < time >ms
	- --badsum
		- bad bad
	- -sn
		- ICMP network sweep
		- can also do subnet masks
		- either ICMP or ARP (sudo'd)
	- **Question - how do you design your system. to best defend it from such?** 
		
- redis-tools
	- installed in Ubuntu (apt install redis-tools)
- GoBuster
	- https://github.com/OJ/gobuster
	- A tool to brute-force:
		- URI (directories and files) in websites
		- DNS subdomains (with wildcard support)
		- Virtual Host names on target web servers
		- Open Amazon S3 buckets
		- Open Google Cloud Buckets
		- TFTP servers
	- Wordlists - generally kept in PATH /usr/share/wordlists, however, you can keep these wherever
	- git clone https://github.com/danielmiessler/SecLists.git = one of the most famous wordlist collections in use today
- Task Manager (Windows)
	- Task Manager is a built-in GUI-based Windows utility that allows users to see what is running on the Windows system. It also provides information on resource usage, such as how much each process utilizes CPU and memory. When a program is not responding, the Task Manager is used to terminate the process. (TryHackMe Endpoint Sec Fundamentals module)
- Lynx - text-based browser for Linux
- mysql
	- -h : connect to a host 
	- Three DB's in each MySQL instance that are common across ALL MySQL instances:
		- information_schema
		- mysql
		- performance_schema
- Windows Powertoys:
  https://learn.microsoft.com/en-us/windows/powertoys/)
- MXToolBox:
  https://mxtoolbox.com/
- NZ Domain Name Commision - WHOIS lookup:
  https://dnc.org.nz/whois/whois-lookup/
- WHOIS lookup:
  https://who.is/
- Parallels (Windows on MacOS)
- DIG - Domain Information Groper (can also get this on Windows via WSL)
- - Sysinternals TCPView
- nmap (for both Unix and Windows shells)
	- nmap -p- --min-rate 1000 -sV 10.129.164.215
- DNSCrypt (https://www.dnscrypt.org/)
	- A protocol that authenticates communications between a DNS client and a DNS resolver. It prevents DNS spoofing. It uses cryptographic singatures to verify that responses originate from the chosen DNS resolver and haven't been tampered with. 
	- (free and open-source implementations - not affiliated with any company or organisation)
- Spectrum Analyzers & Network Scanning Tools
	- WiFi Analyser (for example)
- tee : read from standard input and write to standard output and files
	- -a : appends to the file
	- Example:
		echo "some shit goes at the end of the piped file" | sudo tee -a *filename* 
	- What this does is, it will print out the "some shit.." string and then pipe the tee command to append it into whatever the *filename* is
- vim
	- Text Editor in zshell
- Responder (Python)
	- Tool for:
		- LLMNR
		- NBTNS
		- MDNS poisoning
		- WPAD spoofing
	- It can also be used in 'analyze' mode.
	- Browser mode: inspect "Browse Service" messages and map IP addresses with NetBIOS names. 
		(from thehacker.recipes)
- John-The-Ripper:
	  https://github.com/piyushcse29/john-the-ripper/blob/master/doc/NETNTLM_README
	- One of several tools that can take a NetNTLMv2 challenge/response and try millions of passwords to see if any of them generate the same response. 
- LogicMonitor
	- Enables you to control which users in your account use the REST API, and monitor how often they are using it. 
- evil-winrm
- PGP - Pretty Good Privacy
	- An encryption program that provides cryptographic privacy and authentication for data communication. Used for signing, encrypting and decrypting texts, emails, files, directories, and whole disk partitions and to increase the security of email communications. (created by Philip Zimmerman) 
- EDR - Endpoint Detection and Response tool
	- Used to audit devices for common and known vulnerabilities (I'm thinking against a known and well updated database or several of them)
	- Monitoring a device for suspicious activity
		- Privilege escalations (UACs I'm thinking)
		- Recording normal behaviour of the device to pick up any weird or out of the ordinary anomaly type patterns 
		- Monitoring for suspicious activity
			- Unauthorised logins
			- Brute-force attacks
			- Privilege escalations
- MD5 Hash Generator:
	- https://www.md5hashgenerator.com/
- Base64 Encoder/Decoder:
	- https://www.base64decode.org/
- CVSS Calculator: https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator
- VXUnderground
- OSINT | Exif Tool (https://exif.osint-tool.com/)
	- A tool that allows for viewing hidden metadata in your images
	- Details like 
		- geolocation
		- Camera settings
		- Image Properties
		- And others
  - Lavabit (https://lavabit.com/)
	  A tool to use to encrypt emails
	  Was shut down in 2013, Edward Snowden was known to be using this tool
	  Has been resurrected in 2017
	  Now uses Flow for consumer-grade solutions
	  Enterprise-grade have paid for solutions
  - Protonmail https://proton.me/mail
	  - Opensource alternative to the what is now Lavabit
	  - However you have to signup to be able to use the service (and the free version has slight limitations compared to the paid for ones)
  - WappAlyzer
	  - Can identify the tools used on websites you visit 
- awscli
	- Allows for the interaction with S3 Buckets
- smbclient
	- Speaks with port 445 (Microsoft's SMB) service which allows for shares (printers, files etc)
	- The "backups" share is non-admin'd  (usually)
- impacket (impacket-netview)
	- A python3 tool focused on providing access to network packets
- winPEAS
- PDFinfo
- Mimikatz
	- Used to steal authentication information from compromised Windows computers. 
- DNSDumpster (https://dnsdumpster.com/)
	- Subdomain finderr
- Burp Suite
	- Can act as a proxy between web requests
	- Able to identify website structure and relay this to the requestor amongst other uses
- Reverse Shell Generator
	- revshells.com
- waybackurls (in conjunction with web.archive.org)
	- admin panels
		- site:whatevs.com inurl:admin
	- Le pwords:
		- filetype:log "password" site:whatevs.com
	- backup dirs:
		- intitle:"index of" "backup" site:whatevssss.com
- enum4linux
	- enumerate SMB shares (both on Win and Linux platforms)
- smbclient
- 




- IDEs (Integrated Development Environment)
  *revise these*
	- Obisidian (not really an IDE but I'm putting it in here)
	- VisualStudio
	- Notepad++
	- IntelliJ IDEA
	- Eclipse
	- NetBeans
	- Code::Blocks
	- Aptana Studio 3
	- Xcode
	- Komodo IDE
	- Source-code editor
	- Atom
	- Debugging Tools
	- Integrations
	- Language Support
	- RubyMine
	- Amethyst 2
	- C++
	- Cloud IDEs
	- Compiler
	- Mobile Development
	- HTML (5)
	- Debugger
	- MonoDevelop
	- Python
	- Codenvy
	(these are sourced from the web)
