Tools mainly being used so far in this course will be described here (note - there are HEAPS out there - refer to the Book of "Secret" Knowledge - lel, secret)
*Perhaps put these into their own sections and further expand.
ie Windows applications/software, Other OS applications/software, PowerShell tools, Unix/Linux shell tools - differentiating between the different shells if relevant (bash, zsh etc) - atm this section is all jumbled up*

- Finder
	- Pretty neat, kind of like Finder in MacOS, real fast to search for stuff when compared to your usual File Explorer in Windows
	- voidtools.com
	- Quick filename indexing
- Burp Suite
	- Software security application used for penetration testing of web applications
	- https://portswigger.net/burp
- PuTTY - Pretty Useful Teletypewriter
	- Good way to telnet, SSH so on so forth to machines
- Have I Been Pwned?
	  https://haveibeenpwned.com/
- nmap
	- **-p0- asks Nmap to scan every possible TCP port**, -v asks Nmap to be verbose about it, -A enables aggressive tests such as remote OS detection, service/version detection, and the Nmap Scripting Engine (NSE). Finally, -T4 enables a more aggressive timing policy to speed up the scan. (nmap.org)
	- https://www.stationx.net/nmap-cheat-sheet/
	- -open : Only show open (or possibly open) ports
	- example: nmap -open -p- -T5 *ip_address/hostname*
		- This will scan for all open ports
		- Scanning all ports up to 65535 (max number of possible ports)
		- Trying to go as fast as it can
	- -sV : Probe open ports to determine service/version info
	- -sC : equivalent to --script=default
		- example: nmap -sC -sV *ip_address/hostname*
		- nmap -p- --min-rate 1000 -sV *ipaddress*
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
