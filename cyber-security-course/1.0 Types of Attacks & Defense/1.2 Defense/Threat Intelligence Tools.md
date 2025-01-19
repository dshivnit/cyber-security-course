https://tryhackme.com/r/room/threatinteltools

To mitigate against risks, we can start by trying to answer:
- Who's attacking?
- What is their motivation?
- What capabilities do they have?
- What artefacts and indicators of compromise do we need to identify and look out for?

Threat Intelligence Classifications
	Threat intelligence is geared towards understanding the relationship between your operational environment and your adversary. We can break threat intel into the following classifications:
- Strategic Intel
	- High-level intel that looks into the organisation's threat landscape and maps out the risks based on trends, patterns and emerging threats that may impact business decisions. 
- Technical Intel
	- Looks into evidence and artefacts of attack used by an adversary. 
	- Incident Response teams can use this intel to create a baseline attack surface to analyse and develop defense mechanisms
- Tactical Intel
	- Assesses adversaries' TTPs. 
	- This type of intel can strengthen security controls and address vulnerabilities through real-time investigations
- Operational Intel
	- Looks into an adversary's specific motives and intent to perform an attack. Security teams may use this intel to understand the critical assets available in the organisation (people, processes, and technologies) that may be targeted. 

Now we'll dive into some tools.

- urlscan.io
	- https://urlscan.io/
	- Free service developed to assist in scanning and analysing websites
	- It automates the process of browsing and crawling through websites to record activities and interactions
	- When a URL has been submitted for processing/scanning, the information that gets recorded includes the domains and IP addresses contacted, resources requested from the domains, a snapshot of the main webpage, technologies utilised and other metadata about the website

- Abuse.ch
	- https://abuse.ch/
	- Research project hosted by the Institute for Cybersecurity and Engineering at the Bern University of Applied Sciences in Switzerland
	- Developed to identify and track malware and botnets through several operational platforms developed under the project:
		- Malware Bazaar
			- https://bazaar.abuse.ch/browse/
			- A resource for sharing malware samples
			- An all-in-one malware collection and analysis database
			- Supports:
				- Malware Samples Upload
					- Analysts can upload their malware samples for analysis and build the intelligence database
				- Malware Hunting
					- Hunting for malware samples is possible through setting up alerts to match various elements such as tags, signatures, YARA rules, ClamAV signatures and vendor detection
		- Feodo Tracker
			- https://feodotracker.abuse.ch/
			- A resource used to track botnet command and control (C2) infrastructure linked with Emotet, Dridex and TrickBot
				- Offers various blocklists, helping network owners to protect their users from Dridex and Emotet/Heodo.
				- Provides a database of the C&C servers that security analysts can search through and investigate any suspicious IP addresses they have come across. 
				- They provide various IP and IoC blocklists and mitigation information to be used to prevent botnet infections
		- SSL Blacklist (SSLBL)
			- https://sslbl.abuse.ch/
			- A resource for collecting and providing a blocklist for malicious SSL certificates and JA3/JA3s fingerprints
			- Goal of detection malicious SSL connections, by identifying and blacklisting SSL certificates used by botnet C&C servers
			- Identifies JA3 fingerprints that helps you to detect and block malware botnet C&C communication on the TCP layer
			- SSL certificates used by botnet C2 servers would be identified and updated on a denylist that is provided for use
		- URL Haus
			- https://urlhaus.abuse.ch/
			- A resource for sharing malware distribution sites
			- You can report URLs and explore the database for valuable intelligence
			- Use the APIs to *seamlessly* push and pull signals, and automate bulk queries
			- With this intelligence, one can gain insights into malware behaviour, assist to identify, track and mitigate against malware and botnet-related cyber threats
			- As an analyst, you can search through the database for domains, URLs, hashes and filetypes that are suspected to be malicious and **validate** your investigations
			- It also provides feeds associated with country, AS number and TLD (Top-Level Domain) that an analyst can generate based on specific search needs
		- Threat Fox
			- https://threatfox.abuse.ch/
			- A resource for sharing indicators of compromise (IoCs)
			- A platform dedicated to sharing IoCs (Indicators of Compromise) associated with malware, with the infosec community, AV vendors and cyber threat intelligence providers
			- You can upload IoCs and explore the database for valuable intelligence
			- Analysts can search for, share, and export IoCs associated with malware. IoCs can be exported in various formats such as MISP events, Suricata IDS Ruleset, Domain Host Files, DNS Response Policy Zone, JSON files and CSV files.
		- YARAify
			- https://yaraify.abuse.ch/
			- Allows anyone to scan suspicious files against a large repository of YARA rules to detect malware
			- Scan suspicious malware samples, or process dumps, and explore the database for valuable intelligence
			- Set alerts to hunt for newly observed files, use APIs for scanning, downloads, and automate bulk queries - and also share YARA rules with the community

PhishTool
- https://www.phishtool.com/
- Email analysis tool
- Seeks to elevate the perception of phishing as a severe form of attack and provide a responsive means of email security. 
- Through email analysis, security analysts can uncover email IoCs, prevent breaches and provide forensic reports that could be used in phishing containment and training engagements. 
- Core features (Community version - there is also a Enterprise version as well)
	- Perform email analysis
		- Retrieves metadata from phishing emails and provides analysts with the relevant explanations and capabilities to follow the email's actions, attachments, and URLs to triage the situation
	- Heuristic intelligence
		- OSINT is baked into the tool to provide analysts with the intelligence needed to stay ahead of persistent attacks and understand what TTPs were used to evade security controls and allow the adversary to social engineer a target
	- Classification and reporting
		- Phishing email classifications are conducted to allow analysts to take action quickly. Additionally, reports can be generated to provide a forensic record that can be shared
- Additional features on the ENTERPRISE version:
	- Manage user-reported phishing events
	- Report phishing email findings back to users and keep them engaged in the process
	- Email stack integration with M365 and Google Workspace

Cisco Talos Intelligence
- https://talosintelligence.com/
	Analysts can collect a huge amount of information that could be used for threat analysis and intelligence. Cisco has assembled a large team of security practitioners called Cisco Talos to provide actionable intelligence, visibility on indicators, and protection against emerging threats through data collected from their products. 
	The solution is called, Talos Intelligence
- Encompasses six key teams:
	- Threat Intelligence and Interdiction
		- Quick correlation and tracking of threats provide a means to turn simple IoCs into context-rich intel
	- Detection Research
		- Vulnerability and malware analysis is performed to create rules and content for threat detection
	- Engineering & Development
		- Provides the maintenance support for the inspection engines and keeps them up to-date to identify and triage emerging threats
	- Vulnerability Research & Discovery
		- Working with service and software vendors to develop repeatable means of identifying and reporting security vulnerabilities
	- Communities
		- Maintains the image of the team and the open-source solutions
	- Global Outreach
		- Disseminates intelligence to customers and the security community through publications
- 