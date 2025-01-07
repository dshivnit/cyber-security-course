- Created by Paul Pols' in 2017
- Aims to complement, NOT compete, with other cybersecurity kill chain frameworks, such as the Lockheed Martin's one (Cyber Kill Chain) and MITRE's ATT&CK
- Establishing a good cybersecurity posture
- Understanding an attacker's motivation, methodologies and tactics
- Phases of the Unified Kill Chain
- A framework that is used to complement other frameworks such as MITRE

- Kill Chain
	- A methodology/path that attackers use to approach and intrude a target
- Objective is to understand an attacker's "Kill Chain" so that defensive measures can be put in place to either pre-emptively protect a system, or disrupt an attacker's attempt. 

- Threat Modelling
	- A series of steps to ultimately improve the security of a system.
	- Identifying risk, and essentially boils down to:
		- Identifying what systems and applications need to be secured and what function they serve in the environment
		- ie - is the system critical to normal operations, and is a system holding sensitive information related to PCI or PII
	- Assessing what vulnerabilities and weaknesses these systems and applications may have and how they could be potentially exploited
	- Creating a plan of action to secure these systems and applications from the vulnerabilities highlighted
	- Putting in policies to prevent these vulnerabilities from occurring again where possible 
	- Threat modelling is an important procedure in reducing the risk within a system or application
	- It creates a high-level overview of an organisation's IT assets and the procedures to resolve vulnerabilities
	- Can help identify potential attack surfaces and how these systems may be exploited
	- Some frameworks used in Threat Modelling:
		- STRIDE
			- Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege
		- DREAD
			- Risk Assessment model
			- Quantitative method of calculating the severity of a threat using a scaled grading system so that high severity concerns can be addressed first
		- PASTA
			- Process for Attack Simulation and Threat Analysis
		- CVSS
			- Common Vulnerability Scoring System
			- Public framework for rating the severity and characteristics of security vulnerabilities in information systems
	- 18 Phases:
		- Reconnaissance
			- Researching, identifying and selecting targets using active or passive reconnaissance
		- Weaponisation
			- Preparatory activities aimed at setting up the infrastructure required for the attack
		- Delivery
			- Techniques resulting in the transmission of a weaponised object to the targeted environment
		- Social Engineering
			- Techniques aimed at the manipulation of people to perform unsafe actions
		- Exploitation
			- Techniques to exploit vulnerabilities in systems that may, amongst others, result in code execution
		- Persistence
			- Any access, action or change to a system that gives an attacker persistent presence on the system
		- Defense Evasion
			- Techniques an attacker may specifically use for evading detection or avoiding other defenses
		- Command and Control
			- Techniques that allow attackers to communicate with controlled systems within a target network
		- Pivoting
			- Tunneling traffic through a controlled system to other systems that are not directly accessible
		- Discovery
			- Techniques that allow an attacker to gain knowledge about a system and its environment
		- Privilege Escalation
			- The result of techniques that provide an attacker with higher permissions on a system or network
		- Execution 
			- Techniques that result in execution of attacker-controlled code on a local or remote system
		- Credential Access
			- Techniques resulting in the access of, or control over, system, service or domain credentials
		- Lateral Movement
			- Techniques that enable an adversary to horizontally access and control other remote systems
		- Collection
			- Techniques used to identify and gather data from a target network prior to exfiltration
		- Exfiltration
			- Techniques that result or aid an attacker removing data from a target network
		- Impact
			- Techniques aimed at manipulating, interrupting, or destroying the target system or data
		- Objectives
			- Socio-technical objectives of an attack that are intended to achieve a strategic goal
	- 