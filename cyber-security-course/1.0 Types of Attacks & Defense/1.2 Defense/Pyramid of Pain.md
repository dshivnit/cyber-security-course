(Credit to THM, cmnatic, Dex01 and 1337rce)

- Applied to cybersecurity solutions like Cisco Security, SentinelOne and SOCRadar to improve the effectiveness of Cyber Threat Intelligence (CTI)
- David Blanco - "the amount of pain you cause an adversary depends on the types of indicators you are capable to make use of."

- Hash Values
	- Easily manipulated by adjusting the hash
		- ie adding some text to the end of the file (regardless if it's an executable)
		- Example:
			- `Get-FileHash .\installer.exe -Algorithm MD5`
			- `echo "DestroyHash" >> .\installer.exe`
			- The results from the `Get-FileHash` command will be different
	- This makes it difficult when threat hunting Hashes of files as IoC's (Indicators of Compromise)
	- Use tools like VirusTotal or MetaDefender to review hashes, files and other elements

- IP Addresses
	- Fast Flux
		- A technique used by cybercriminals to increase their infrastructure's resilience by making law enforcement takedown of their servers and deny listing of their IP addresses harder
		- To hide malware delivery and phishing websites by rapidly cycling through IP addresses tied to a malicious domain
		- A DNS technique used by botnets to hide phishing, web proxying, malware delivery, and malware communication activities behind compromised hosts acting as proxies
		- Purpose is to make communication between malware and its C&C server challenging to be discovered by security professionals
	- Domain Fluxing
		- Technique in which domain names of the server involved with malicious activities is changed constantly - thus obscuring threat actors operations
	- In a single-flux network, the authoritative name server of a fast-flux domain name continuously permutes DNS records with short TTL values - usually between 180 and 600 seconds
	- Any.run (and similar tools)
		- Running malicious software against tools like any.run will allow cyber defense analysts to analyse for open connections and requests to both IP addresses and Domain Names 
		- Analysts will then be able to determine whether these connections are valid or not and will be able to look into the backgrounds of said domains and IP addresses further

- Domain Names
	- Some (a lot) of DNS providers have loose standards and provide APIs to make it easy for *people* to change the domain
	- Punycode
		- A way of converting words that cannot be written in ASCII, into a Unicode ASCII encoding
		- https://www.jamf.com/blog/punycode-attacks/
	- To detect malicious domains, proxy logs or web server logs can be used
	- Threat actors usually hide malicious domains under URL shorteners
	- URL Shortener
		- Tool that creates a short and unique URL tha twill redirect to the specific website specified during the initial step of setting up the URL shortener link
	- Any.run
		- Sandboxing service that executes file samples
		- You can review connections such as HTTP requests, DNS requests, or processes communicating with an IP Address

- Host Artifacts
	- Host artifacts are the traces or observables that attackers leave on the system, such as registry values, suspicious process execution, attack patters or IoCs, files dropped by malicious applications, or anything exclusive to the threat

- Network Artifacts
	- A network artifact can be a user-agent string, C2 information, or URI patterns followed by the HTTP Post request. 
	- An attacker might use a User-Agent string that hasn't been observed in your environment before or seems out of the ordinary 
	- Network artifacts can be detected in Wireshark's PCAPs
		- Or using Network Protocol Analysers like TShark
		- Or IDS logs (such as Snort)
			- https://www.snort.org/
	- If you can detect custom User-Agent strings that an attacker is uing, you might be able to block them
	- Creating more obstacles and making their attempt to compromise the network more annoying

- Tools
	- MalwareBazaar
		- https://bazaar.abuse.ch/
	- MalShare
		- https://malshare.com/
	- SOC Prime Platform
		- https://tdm.socprime.com/
	- ssdeep
		- https://ssdeep-project.github.io/ssdeep/index.html
		- Fuzzy hashing (Context Triggered Piecewise Hashes - CTPH)
		- Helps perform similarity analysis of hashes
		- Match two files with minor differences based on the fuzzy hash values

- TTPs
	- MITRE ATT&CK Matrix
		- https://attack.mitre.org/