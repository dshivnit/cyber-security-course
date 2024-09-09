- Kill Chain
	- A military concept related to the structure of an attack. 
	- Consists of target identification, decision, and order to attack the target, and finally the destruction of the target
- Cyber Kill Chain Framework
	- Lockheed Martin - A global security aerospace company 
	- Established the framework for the cybersecurity industry in 2011
	- Based on the military concept above
	- Defines steps used by threat actors in cyberspace
	- To succeed, an adversary needs to go through all phases of the Kill Chain. 
- The Cyber Kill Chain will help you understand and protect against attacks (ransomware, security breaches) as well as APTs. 
- It can be used to assess the network and system security by identifying missing security controls and closing certain security gaps based on the company's infrastructure (Gap Analysis)
- By understanding the Kill Chain as a SOC analyst, Security Researcher, Threat Hunter or Incident Responder - you will be able to recognise the intrusion attempts and understand the intruder's goals and objectives

- Phases:
	- Reconnaissance
	- Weaponisation
	- Delivery
	- Exploitation
	- Installation
	- Command & Control
	- Actions on Objectives

Reconnaissance
- Reconnaissance
	- Discovering and collecting information on the system and the victim. The reconnaissance phase is the planning phase for the threat actor(s)
- OSINT
	- Open-Source Intelligence, also falls under recon. The first step an attacker needs to complete to carry out the further phases of an attack. The attacker needs to study the victim by collecting every available piece of information on the company and its employees, such as the company's size, email addresses, phone numbers from publicly available resources to determine the best target for the attack
- Email Harvesting
	- the process of obtaining email addresses from public, paid, or free services. 
	- An attacker can use email-address harvesting for phishing attacks to steal sensitive data (logins, credit cards numbers, and so on)
	- The Harvester
		- Also capable of gathering names, subdomains, IPs, and URLs using multiple public data sources
	- Hunter.io
		- Email hunting tool that will let you obtain contact information associated with the domain
	- OSINT Framework
		- provides the collection of OSINT tools based on various categories
- Social Media
	- Services such as LinkedIn, Facebook, Twitter and Instagram can be used to collect information on individuals and companies

Weaponisation
- The threat actor would create a "weaponiser" - which would combine malware and exploit into a deliverable payload. So as to not interact with the victim directly
- Most attackers would use automated tools to generate the malware or refer to the DarkWeb to purchase said malware
- More sophisticated actors, or state-sponsored APTs would write their own custom malware to make the sample unique and evade detection on the target
- Malware
	- A program or software that is designed to damage, disrupt, or gain unauthorised access to a computer
- Exploit
	- A program or a code that takes advantage of the vulnerability or flaw in the application or system
- Payload
	- A malicious code that the attacker runs on the system
- The attacker could:
	- Create an infected MS Office document containing a malicious macro or VBA script
	- Create a malicious payload or a very sophisticated worm, implant it on the USB drives and then distribute them in public - virus
	- Choose C2 (Command and Control) techniques for executing the commands on the victim's machine or deliver more payloads
	- Select a backdoor implant (the way to access the computer system, which includes bypassing the security mechanisms)

Delivery
- Phishing email
	- Targeting a specific person or multiple people in the company
- Distributing infected USB drives/devices
- Watering hole attack
	- Targeted attack designed to aim at a specific group of people by compromising the website they are usually visiting and then redirecting them to the malicious website of an attacker's choice
	- The threat actor would look for a known vulnerability for the website to try to exploit it
	- They would encourage the victims to visit the website by sending 'harmless' emails pointing tout the malicious URL to make the attack work more efficiently 
	- After visiting the website, the victim would unintentionally download malware or a malicious application to their computer
	- This type of attack is called a drive-by download
	- An example: a malicious pop-up asking to download a fake Browser extension

Exploitation
- Exploit the vulnerability
- Lateral Movement
	- Refers to the techniques that a malicious actor uses after gaining initial access to the victim's machine to move deeper into a network to obtain sensitive data
- Zero-day Exploit
	- An unknown exploit in the wild that exposes a vulnerability in software or hardware and can create complicated problems well before anyone realises something is wrong. 
	- Leaves no opportunity for detection at the beginning
- How a threat actor could carry out an exploit:
	- Victim triggers the exploit by opening an email attachment or clicking on a malicious link
	- Using a zero-day exploit
	- Exploit software, hardware, or even human vulnerabilities
	- Attacker triggers the exploit for server-based vulnerabilities

Installation
- Backdoor can also be referred to as an access point (not a WAP)
- Once an attacker gets into a system, they may want to re-access the system if they lose connection to it or if detected, or if the system is later patched
- Persistent backdoor
	- Will allow the attacker access to the system they compromised in the past
	- Can be achieved through:
		- Installing a web-shell on the webserver
			- A malicious script written in web development programming languages such as ASP, PHP, or JSP used by an attacker to maintain access to the compromised system
			- Because of the web shell simplicity and file formatting, can be difficult to detect and might be classified as benign
		- Installing a backdoor on the victim's machine
			- Using Meterpreter to install a backdoor on the victim's machine
			- Meterpreter - a Metasploit Framework payload that gives an interactive shell from which an attacker can interact with the victim's machine remotely and execute malicious code
		- Creating or modifying Windows services
			- Known as T1543.003 on MITRE ATT&CK
			- An attacker can create or modify the Windows services to execute the malicious scripts or payloads regularly as part of the persistence. 
			- Threat actors could use tools like sc.exe (which allows you to create, start, stop, query or delete any Windows Service) and Reg to modify service configurations
			- The attacker can also masquerade the malicious payload by using a service name that is known to be related to the OS or legitimate software
		- Adding the entry to the "run keys" for the malicious payload in the Registry or the Startup Folder
			- By doing so, the payload will execute each time the user logs on to the computer
			- There are startup folders/locations for individual users and also the entire system
	- Timestomping Technique
		- To avoid detection by forensic investigators to make malware appear as part of a legitimate program
		- Lets an attacker modify the file's timestamps, including the modify, access, create and change times

Command and Control (C2, C2 Beaconing)
- Allows threat actor(s) to remotely control and manipulate the infected/targeted machine
- A type of malicious communication between a C&C server and malware on the infected host.
- The infected host will consistently communicate with the C2 server, that is also where the term 'beaconing' came from
- The compromised endpoint would communicate with an external server set up by an attacker to establish a C&C channel
- After establishing the connection, the attacker has full control of the victim's machine
- Until recently, IRC (Internet Relay Chat) was the traditional C2 channel used by threat actors
	- This is no longer the case as modern security solutions can easily detect malicious IRC traffic
- The most common C2 channels used by adversaries:
	- Port 80 and 443
		- Blends the beaconing malicious traffic with the legitimate traffic and can help the attacker evade firewalls
	- DNS
		- Infected machine makes constant DNS requests to the DNS server that belongs to an attacker, this type o C2 communication is also known as DNS Tunneling.

Actions on Objectives (Exfiltration)
- Taking action on the threat actor's original objectives
- The following could be achieved:
	- Collect credentials from users
	- Perform privilege escalation (gaining elevated access like domain admin access from a workstation by exploiting the misconfiguration)
	- Internal reconnaissance (for example, an attacker gets to interact with internal software to find its vulnerabilities)
	- Lateral movement through the company's environment
	- Collect and exfiltrate sensitive data
	- Deleting the backups and shadow copies
	- Overwrite or corrupt data

Cyber Kill Chain can be a great tool to improve network defence, but it is only one to consider and should not be the only one to rely on. 
Need to have a look at other kill chain methods and alternatives as well. 

Cybersecurity threats have developed drastically in today's time, and adversaries are combining multiple TTPs to achieve their goals. 

Cyber Kill Chain would not be able to identify insider threats. 

Consider the MITRE ATT&CK Framework as well as the Unified Kill Chain to apply a more comprehensive approach to defense methodologies.