*All of these will need to be revised, updated and added to*
[[1.1.1 Types of Attacks]]

[[1.2.1 Types of Defense]]

[[Open-Source Intelligence (OSINT)]]

- Heap Corruption
- 
- Vulnerabilities
	- A weakness or flaw in the design, implementation or behaviours of a system or application. 
	- NIST defines, "weakness in an information system, system security procedures, internal controls, or implementation that could be exploited or triggered by a threat source." 
	- Most common types:
		- Operating System
			- Normally resulting in privilege escalation
		- (Mis)Configuration-based
			- Incorrectly configured application and/or service
		- Weak or Default Credentials
			- GG speaks for itself
		- Application Logic
			- Poorly designed applications
			- ie - poorly implemented Authentication Systems/Mechanisms (where in an attacker can impersonate a User)
		- Human-Factor
			- ie phishing emails
			- Layer 8s
- Vulnerability Management
	- Evaluating, categorising, and ultimately remediating threats (vulnerabilities) faced by an organisation. 
	- It is arguably impossible to patch and remedy every single vulnerability in a network or computer system and sometimes a waste of resources. 
	- Approximately 2% of vulnerabilities only ever end up being exploited (Kenna Security 2020). 
	- It is all about addressing the MOST EDANGEROUS vulnerabilities and reducing the likelihood of an attack vector being used to exploit a system. 
	- Common Vulnerability Scoring System (CVSS)
		- Scores based upon features, availability and reproducibility
		- Introduced in 2005
		- Current version CVSSv3.1 (4.0 in draft)
			- How easy is it to exploit the vulnerability?
			- Do exploits exist for this? 
			- How does this vulnerability interfere with the CIA triad?
				- CIA Triad - a framework that combines three key information security principles: Confidentiality, Integrity and Availability (coursera.org)
		- CVSS Calculator: https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator
				  (from TryHackMe)
	- Vulnerability Priority Rating (VPR)
		- More modern framework in vulnerability management - developed by Tenable (an industry solutions provider for vulnerability management)
		- Considered to be risk-driven
			- HEAVY FOCUS on the risk a vulnerability poses to the organisation itself, rather than factors such as impact (like with the CVSS)
		- Intended for a commercial platform as the Vulnerability Priority Rating (VPR) system is not open-source
		- Considers over 150 factors when considering and calculating risks
		- Helps Security Engineers prioritise patching vulnerabilities
		- Scores are not final and dynamic - initial score will change over time as the vulnerability ages
		- Does not consider Confidentiality, Integrity and Availability (the CIA Triad) of vulnerabilities.
- Vulnerability Databases
	- Resources on the Internet that keep track of vulnerabilities for all sorts of software, operating systems and other systems/services
	- National Vulnerability Database (NVD)
	- Exploit-DB
	- Consider:
		- Vulnerability and its definition : weakness or flaw in the design, implementation and behaviours of a system
		- Exploit : action or behaviour that utilises a vulnerability in a system, service or application
		- PoC (Proof of Concept) - technique or tool that demonstrates the exploitation and/or vulnerability
	- National Vulnerability Database (NVD) (https://nvd.nist.gov/)
		- A website that lists all publicly categorised vulnerabilities. 
		- Not the best for searching or filtering your queries to a specific application and/or threat
	- Exploit-DB (https://exploit-db.com)
		- A resource that CyberSec analysts will find more helpful
		- Retains exploits for software and applications stored under the name, author and version of the software application
		- You can use it to look for snippets of code (PoC's) that are used to exploit a specific vulnerability
		- Database was started in 2004 by a hacker group known as milw0rm
		- However, other sources say that it is OffSec who maintain it and are seen as the author of the DB
	- Version Disclosure
		- When one version of an application has exploits that have been identified perhaps sometimes released for public information
		- 