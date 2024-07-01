Tools mainly being used so far in this course will be described here (note - there are HEAPS out there - refer to the Book of "Secret" Knowledge - lel, secret)
*Perhaps put these into their own sections and further expand.*

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
- 