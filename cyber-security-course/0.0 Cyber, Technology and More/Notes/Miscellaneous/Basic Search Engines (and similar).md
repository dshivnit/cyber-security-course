- Search Operators
	- `"exact phrase"`
		- Indicate that you are looking for an exact word or phrase (between the double quotes)
	- `site:`
		- Lets you specify the domain name to which you want to limit your search
		- For example - if we wanted to search the nzherald.co.nz website for something in particular:
			- `site: nzherald.co.nz today's daily quiz`
	- The minus symbol (`-`)
		- Allows one to trunc/omit results from a search that contain a word or phrase, or even a website
		- Say for example:
			- `"today's news" -nzherald.co.nz -business`
	- `filetype:`
		- Used when wanting to find files instead of pages in a search result
		- Consider a file type when doing so 
			- `filetype:jpg "pictures of cats"`
	- For more visit: https://github.com/cipher387/Advanced-search-operators-list
	- `man [linux-command]` 
		- Usually will return the man page for the given command, can be handy :) 

- Shodan
	- https://www.shodan.io/
	- Searches for devices connected to the Internet
	- One can search for specific types and versions of servers, networking equipment, industrial control systems, IoT devices, etc
	- Say for example if you want to search for a web-server version of Apache that is outdated or a version of it that has been known to be compromised but is still in use... This is where you can do it
	- https://www.shodan.io/

- Censys
	- https://search.censys.io/
	- This engine focuses on hosts, websites, certs, and other assets connected to the Internet
	- Enumerating Domains that are in use
	- Checking open ports and their services
	- For discovering assets within a network, consider:
		- https://support.censys.io/hc/en-us/articles/20720064229140-Censys-Search-Use-Cases

- VirusTotal
	- https://www.virustotal.com/gui/home/upload
	- An online tool that can be used as a virus/malware scanning service for files - it uses multiple engines to do so, give it a go
	- Not just for files, but also for URLs, Hashes, IP Addresses - give it a go and see the results you get
	- A lot of community input is involved - which can be good. 

- Have I Been Pwnd
	- Checks an email address to see if it has been associated with any compromised system online
	- If it has been - then it is likely that the same email address could potentially have used the same password for other systems online
	- It's a good idea to use Password Managers which allow you to use complex passwords for every single account you choose to login with using the same email address
		- Example: KeePassXC (https://keepassxc.org/)

- CVEs (Common Vulnerabilities and Exploits)
	- Consider these repositories as a collection of known vulnerabilities that have come to be.
	- A lot of the time a CVE repo will show you the affected systems, root of the issue and what impact it has with a severity level rating (the higher the score, the higher the risk of it and nature of it being exposed to the general public and businesses)
	- Usually solution and investigating research teams will create a proof of concept (POC) of the exploit and advise what the solution may have been if the CVE had been resolved
		- Normally these solutions would be the patching of said system by its developer
	- You will see:
		- A CVE ID (which identifies the CVE - normally categorised by the year it was identified and then its identifier) 
		- The MITRE Corporation maintains the CVE system
	- There are various solutions to search for known CVEs online -  examples:
		- https://www.cvedetails.com/vulnerability-list/published_since-last30days/
		- https://www.opencve.io/
		- Toggle with the filters and search filter settings to get what you actually are looking for

- Exploit Database
	- https://www.exploit-db.com/
	- **Only exploit systems if you have been granted permission by said system's owner**
		- **aka, don't be a f%$@ing idiot**
	- You can search for various systems, versions and known exploit in this database
	- The name speaks for itself

- GitHub
	- https://github.com/
	- Normally an online platform used for software development and somewhat a version control/management tool (online)
	- Also can be a considered a repository for tools (software, scripts, things) that can be used for various reasons, documentation for various things such as publications/descriptions of concepts (such as ethical hacking :) )
	- If you're reading this then you're on GitHub already anyway, but I guess for someone else reading (if that'll ever happen lel)

