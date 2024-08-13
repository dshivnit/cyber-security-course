- Defining Risk
	- The likelihood of a threat actor taking advantage of a vulnerability by using a threat against an IT asset
- Assets
	- Any part of an IT infrastructure that has value
		- Data
		- Equipment
			- Servers, Printers, Computer etc
		- People
		- Services
- Likelihood
	- The probability of assets being damaged over time
	- The probability of an event occurring over time
- Threat Actors
	- Anyone or anything with the motive and resources to attack another's IT Infrastructure
		- Hackers
		- Hacktivists
		- Script Kiddies
		- Insiders
		- Competitors
		- Shadow IT
		- Criminal Syndicates
		- Advanced Persistent Threat (APTs)
			- Long-term hacking of a system to gain information over time (extended)
- Vulnerabilities
	- Weakness inhered in the protection of an asset
- Threat
	- An action (exploit) by a Threat Actor that they can use against a Vulnerability to cause harm to an Asset
- Remediation
	- What Risk Management is ALL ABOUT! :D 
	- What do we do to to prevent the dangerous stuff above (Assets shouldn't be dangerous - unless you tie people and insiders together, then goodbad=bad)

- CIA Triad
	- Confidentiality\
		- Usually comes with forms of encryption
	- Integrity
		- Usually comes with the forms of hashing
	- Availability\
		- Making sure that systems are available when we need them

- Attack Vectors
	- Pathways to gain access to infrastructure
		- Weak configs
		- Open firewall ports
		- Lack of User security awareness
		- Lack of MFA
		- Missing patches
		- Infected USB thumbdrives
	- Supply-chain Attacks
		- Manufacturers
		- Contractorts
		- Implementers
		- Outsourced software development
			- Right-to-audit clause
			- To make sure that those developers/applications are compliant with regulations and security standards

- Threat Intelligence
	- Explain the different Threat Actors, Vectors and Intelligence Sources
	- Facilitate Risk Management
	- Hardening can reduce incident response time
	- Provide Cybersecurity insight:
		- Adversary TTPs (Tactics, Techniques and Procedures)
	- Threat Maps
		- Geographical representation of Malware Attacks
			- https://threatmap.checkpoint.com/
	- Threat Intelligence Sources
		- Closed/Proprietary
			- Signup Services
			- Paid-for Services
		- OSINT (Open-Source Intelligence)
			- Government Reports
			- Media Reports
			- Academic Reports
			- Google Open-source Hacking DB
			- File/Code Repositories
				- GitHub
			- Vulnerability Databases
				- OpenCVE
				- Mitre CVE
				- etc
		- Dark Web/Net
			- Tor Network
			- Encrypted Anonymous Connections
			- Not indexed
				- Journalists
				- Law
				- Government

- Threat Intelligence Sharing 
	- Automated Indicator Sharing (AIS)
		- Exchange of Cybersecurity Intelligence (CI) between entities
	- Structured Threat Information eXpression (STIX)
		- A form of AIS
		- Data exchange format for Cybersecurity Intelligence
	- Trusted Automated eXchange of Intelligence Information (TAXII)
		- Liks an RSS feed, but for threats
		- Consists of TAXII Servers and Clients
		- Real-time Cyber Intelligence feeds

- Risk Management Concepts
	- Risk Vectors
		- Mission-critical IT Systems
			- Payment processing
			- Human resources
			- Emergency systems
		- Sensitive Data
			- Do we know what we have and where it is?
		- Third-party Access
			- Components
			- Entities
				- Contractors, externals etc
	- Physical Risk Vectors
		- Access Control Vestibules
			- Mantraps
				- Getting into a facility (physically)
			- Locked rooms
				- Server rooms
				- Racks 
			- Limited use of Removable MEdia (ie USBs)
	- Risk Management Frameworks (RMFs)
		- Centre for Internet Security (CIS)
		- National Institute of Standards and Technology (NIST - in the USA)
		- NIST RMF 
			- Also known as the Cybersecurity Framework (or CSF)
		- International Organisation for Standardisation/International Electrotechnical Commission (ISO/IEC)
		- Statement on Standards for Attestation Engagements System and Organisation Controls (SSAE SOC 2)
			- Financial statement integrity
			- Internal controls
			- Type I and Type II
			- Look at different methods to control access to Processes and resulting Financial Documents within an organisation  
		- NIST Special Publication SP 800-30 Rev 1
			- The guide for conducting Risk Assessments
		- Security Regulations and Standards
			- Designed to protect sensitive data
			- GDPR
				- General Data Protection Regulation
			- HIPAA
				- Health Insurance Portability and Accountability Act
			- PCI DSS
				- Payment Card Industry Data Security Standard
				- Protects cardholder information
		- Organisation Security Policies
			- Designed to protect assets
			- AUPs
				- Acceptable Use Policies
					- Define how IT Info Systems are used by Users of an organisation
			- Resource Access Policies
				- App or file access
			- Account Policies
			- Data Retention Policies
				- Usually dictated by regulations/legal 
			- Change Control Policies
			- Asset Management Policies

- Security Controls
	- A solution that mitigates threat
		- ie: Malware scanner mitigates malware infections
	- Implemented differently based on the platform/vendor/user
		- ie Network infrastructure devices
			- Switches, routers, firewalls etc
	- Security Control Categories
		- Managerial/administrative
			- What should be done?
			- Employee background checks
		- Operational
			- How often do we do it? 
			- Periodic review of security policies
		- Technical
			- How will we do it?
			- ie Firewall configurations/rules
	- Security Control Types
		- Physical
			- Access control vestibule (or mantraps)
				- Automatic of closing of doors/gates to prevent tail-gating
		- Detect/ive
			- ie Log analysis
		- Corrective
			- ie Patching known vulnerabilities of systems
		- Deterrent
			- Device logon warning banner
		- Compensating
			- They're normally the second pick
			- When some solutions are usually too expensive, or complicated to implement
			- We compensate by using a secondary option, alternative option
	- Cloud Security Control Documents
		- Cloud Security Alliance (CSA)
	- Risk Examples:
		- Theft of online banking credentials
		- Attack Vectors:
			- Spoofed E-mail message with link to spoofed Web-site tricking an end user
			- Phishing
		- Security Controls
			- User security awareness ... Education
			- Anti-virus software
			- Spam filters

- Risk Assessments and Treatments
	- Prioritising threats against assets of an organisation and then determining what to do about them
	- Can be applied to the whole organisation 
	- Can be applied to a single project or department
	- Could be for specific devices, or network of systems, section of the system
		- Servers
		- Legacy Systems
		- IP - Intellectual Property
		- Software Licensing
			- Is what is being used licensed and adhering to legal requirements, compliance? 
	- Process
		- Risk awareness
			- Cybersecurity intelligence sources
		- Evaluate security controls
			- Inherent (current) and residual risk
		- Implement security controls
		- Review periodically
			- Continuous monitoring
	- Risk Types:
		- Environmental 
			- A natural disaster, event, power outages
		- Person-made
			- Riots
			- Terrorism, sabotage etc
		- Internal
			- Malicious insider, malware infections
			- Unaware Users (untrained)
		- External
			- Competitors
			- Other nation states
	- Risk Treatments
		- Mitigation/reduction
			- Security controls are proactively put in place before undertaking the risk
		- Transference/sharing
			- Some of the risk is transferred to another party
				- ie Insurance
		- Avoidance
			- Avoid an activity because it is too risky
		- Acceptance
			- We accept the risk, it falls within the company's risk appetite

- Quantitative Risk Assessments
	- Attaining budget to be able to implement Security Controls can be a difficult task and process
	- In order to better present requirements/solutions/findings we need to:
		- Summarise risk management processes and concepts
			- Is what is being proposed worth doing?
	- Based on numeric values
	- Identifying Asset Value (AV) 
	- Identifying the Exposure Factor (EF)
		- The percentage of AV loss when a negative incident occurs
		- An EF of 1, which means 100%, would mean a complete and total loss of the Asset in question
	- Single Loss Expectancy (SLE)
		- How much loss is experienced during one negative incident
		- Multiply the AV by the EF
		-  ie 
			- AV = $24,000NZ
				- Say for example how much a Web-system makes on a daily basis, on average
			- What if said Web-system were to go down for three hours in a day for an unexpected reason, due to a particular risk?
				- That would equate to 3/25 = .125 * 100 = 12.5
			- EF = 12.5% (how much loss we'd expect, from a single negative incident)
			- 24000 x 0.125
				- = $3000NZ (SLE)
				- This is how much that downtime would cost, the SLE
		- This is important in Quantitative Risk Assessments
		- Annualised Rate of Occurrence (ARO)
			- Expected n umber of yearly occurrences
				- say, 2-3 times a year
		- Annualised Loss Expectancy (ALE)
			- ALE = SLE x ARO
			- In the example above that would be 3000 x 3 = 9000NZD p/year
		- You then want to compare how much that loss is, compared to how much would be invested/spent on setting up and placing Security Controls into effect
			- So it'd make sense to spend $6000 or less, to protect that Web-system Asset

- Qualitative Risk Assessments
	- Summarise risk management processes and concepts
	- Based on subjective opinion as opposed to hard numbers
		- Threat likelihood
		- Impact of realised threat
		- Severity ratings
	- Depends on who is conducting the Qualitative assessment
	- Risk Register
		- Orgs should have at least one, if not more
		- Centralised list of:
			- Risks
			- Severities
			- Responsibilities
			- Mitigations
	- Usually have a rating system involved
	- Risk Heat Map
		- Allows us to take the severity level for our risks from a Risks Register and put them into a visually compelling type of graph with colour levels can imply the level of risk
			- Red Severe, High
			- Yellow, Medium
			- Green, Low
	- Risk Matrix

- Business Impact Analysis (BIA)
	- Allows us to prioritise Mission Critical Processes
		- Examples
			- Payment processing systems
			- Customer/patient records
				- (Personal Identifiable Information)
	- Assess Risk
		- Identify sensitive data
		- Where is the data that is covered, looked at by compliance/regulatory bodies (law)
		- Identify single points of failure
		- Identify security controls that can be put into place and compliance
	- Examples of impact:
		- Financial
			- Fines
			- Loss of contracts
				- Due to the loss of confidence in the organisation
		- Reputation loss
		- Data loss
			- Breach notification
			- Escalation requirements
				- Law enforcement
				- Government
				- etc
			- Exfiltration
				- Into the hands of unauth'd Users
		- Failed Component Impact
			- MTBF - Mean Time Between Failures
				- Average time between repairable component failures
				- Software patching
			- MTTF - Mean Time To Failure
				- Applies to non-repairable components
				- Drives, switches, routers, motherboard
				- A measure of time until we might expect this kind of failure
			- MTTR - Mean Time To Repair
				- The mean time to repair a component 

	- Locating Critical Resources
		- Where is the data?
		- Data discovery and classification
			- Where is the sensitive data
			- PTA - Privacy Threshold Assessment
				- When you want to understand the nature of the data that you have and the laws and regulations that may apply (compliance)
	- Impact of Sensitive Data
		- Privacy Impact Assessment (PIA)
		- Regulatory compliance
	- RPO - Recovery Point Objective
		- The maximum tolerable amount of data loss
		- Directly related to backup frequency
		- If your RPO is one hour (if we can accommodate for one hour of data loss) then you'd want to ensure that backups are taking place every hour
	- RTO - Recovery Time Objective
		- How much time can we tolerate of downtime of the asset
		-  Return systems and data to usable state within the RTO

- Data Types and Roles
	- 