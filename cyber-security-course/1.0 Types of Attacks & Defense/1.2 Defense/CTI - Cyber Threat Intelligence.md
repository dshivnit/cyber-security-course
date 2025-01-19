https://tryhackme.com/r/room/cyberthreatintel

CTI - Cyber Threat Intelligence
- Can be defined as evidence-based knowledge about adversaries, including their indicators, tactics, motivations, and actional advice against them

Some Terms
- Data - discrete indicators associated with an adversary
	- Such as IP addresses, URLs or hashes
- Information
	- Combination of multiple data points that answer questions such as "how many times has this URL been accessed within the last week?"
- Intelligence
	- The correlation of data and information to extract patterns of actions based on contextual analysis

The primary goal of CTI is to understand the relationship between your operational environment and your adversary and how to defend your environment against any attacks. Develop the cyber threat context by identifying:
- Who's attacking
- What are their motivations
- What are their capabilities
- What artefacts and IoC's should you look out for

Threat intelligence would be gathered from different sources under:
- Internal
	- Corporate security events such as vulnerability assessments and incidence response reports
	- Cyber awareness training reports
	- System logs and events
- Community
	- Open web forums
	- Dark web communities for cybercriminals
- External
	- Threat intel feeds (Commercial & Open-source)
	- Online marketplaces
	- Public sources include government data, publications, social media, financial and industrial assessments

Threat Intelligence Classifications
	Threat Intel is geared towards understanding the relationship between your operational environment and your adversary.
	We can break down TI into these classifications:
		- Strategic Intel
			High-level intel that looks into the organisation's threat landscape and maps out the risk areas based on trends, patterns and emerging threats that may impact business decisions
		- Technical Intel
			Looks into evidence and artefacts of attacks used by an adversary.
			Incident response teams can use this intel to create a baseline attack surface to analyse and develop defense mechanisms
		- Tactical Intel
			This intel will assess an adversaries' TTPs
			Can help to strengthen security controls and address vulnerabilities through real-time investigations
		- Operational Intel
			Looks into an adversary's specific motives and intent to perform an attack. 
			Security teams may use this intel to understand the critical assets available in the organisation (people, processes, and technologies) that may be targeted

CTI Lifecycle
	Threat intel is obtained from a data-churning process that transforms raw data into contextualised and action-oriented insights geared towards triaging security incidents. 
The transformational lifecycle follows a six-phase cycle:
- Direction
	- Every threat intel program will have to have objectives and goals defined, involving identifying the following parameters:
		- Information assets and business processes that require defending
		- Potential impact to be experienced on losing the assets or through process interruptions
		- Sources of data and intel to be used towards protection
		- Tools and resources that are required to defend the assets
	- This phase also allows security analysts to pose questions related to investigating incidents
- Collection
	- Once clear objectives have been defined - security analysts will gather the required data to address them.
	- Analysts will do this by using commercial, private and open-source resources available. 
	- Due to the volume of data analysts usually face, it is recommended to automate this phase to provide time for triaging incidents
- Processing
	- Raw logs, vulnerability information, malware, and network traffic usually come in different formats and may be disconnected when used to investigate an incident. 
	- This phase ensures that the data is extracted, sorted, organised, correlated with appropriate tags and presented visually in a usable and understandable format to the analysts.
	- SIEMs are valuable tools for achieving this and allow quick parsing of data
- Analysis
	- Once the information aggregation is complete, security analysts must derive insights. Decisions to be made may involve:
		- Investigating a potential threat through uncovering indicators and attack patterns
		- Defining an action plan to avert an attack and defend the infrastructure
		- Strengthening security controls or justifying investment for additional resources
- Dissemination
	- Different organisational stakeholders will consume the intelligence in varying languages and formats
	- For example
		- C-Suite members will require a concise report covering trends in adversary activities, financial implications and strategic recommendations.
		- At the same time, analysts will more likely inform the technical team about the threat IOCs, adversary TTPs and tactical action plans
	- CTI is also distributed to organisations using published threat reports. 
		- These reports come from technology and security companies that research emerging and actively used threat vectors.
		- They are valuable for consolidating information presented to all suitable stakeholders. 
		- Some notable threat reports come from:
			- Mandiant
				- https://cloud.google.com/security/resources
			- Recorded Future
				- https://www.recordedfuture.com/resources
			- AT&T Cybersecurity (now referenced as LevelBlue it seems)
				- https://levelblue.com/
- Feedback
	- Final phase and one, if not the most crucial
	- As analysts rely on the responses by stakeholders to improve the threat intelligence process and implementation of security controls
	- Feedback should be a regular interaction between teams to keep the lifecycle working. 

CTI Standards and Frameworks
	Standards and frameworks provide structures to rationalise the distribution and use of threat intel across industries. They also allow for common terminology, which helps in collaboration and communication. The following are some commonly used frameworks:
- MITRE ATT&CK
	- A KB of adversary behaviour, focusing on the indicators and tactics
	- Security analysts can use the information to be thorough while investigating and tracking adversarial behaviour
- TAXII
	- https://oasis-open.github.io/cti-documentation/taxii/intro
	- The Trusted Automated eXchange of Indicator Information (TAXII)
	- OR
	- Trusted Automated eXchange of Intelligence Information (should be this one)
	- Define protocols for securely exchanging threat intel to have near real-time detection, prevention and mitigation of threats
	- The protocol supports two sharing models:
		- Collection
			- Threat intel is collected and hosted by a producer upon request by users using a request-response model
		- Channel
			- Threat intel is pushed to users from a central server through a publish-subscribe model
- STIX
	- https://oasis-open.github.io/cti-documentation/stix/intro
	- Structured Threat Information Expression
	- A language and serialisation format used to exchange CTI
	- Open-source and free allowing those interested to contribute and ask questions in a free manner
	- A language developed for the "specification, capture, characterisation and communication of standardised cyber threat information."
	- Provides defined relationships between sets of threat info such as observables, indicators, adversary TTPs, attack campaigns and more
- Cyber Kill Chain
	- Lockheed Martin's development
	- Breaks down adversary actions into steps:
		- Reconnaissance
		- Weaponisation
		- Delivery
		- Exploitation
		- Installation
		- Command and Control
		- Actions on Objectives
- The Diamond Model
	- Looks at intrusion analysis and tracking attack groups over time
	- Focuses on four key areas, each representing a different point on the diamond:
		- Adversary
			- The focus here is on the threat actor behind an attack and allows analysts to identify the motive behind the attack
		- Victim
			- The opposite end of adversary looks at an individual, group or organisation affected by an attack
		- Infrastructure
			- The adversaries' tools, systems and software to conduct their attack are the main focus
			- Additionally, the victim's systems would be crucial to providing information about the compromise
		- Capabilities
			- Focus here is on the adversary's approach to reaching its goal
			- This looks at the means of exploitation and the TTPs implemented across the attack timeline
	- An Adversary will use a Capability on a given Infrastructure to target a Victim. 
	- Example:
		- An adversary targeting a victim using a phishing attack to obtain sensitive information and compromise their system. 
	- As a threat intelligence analyst, the model allows you to pivot along its properties to produce a complete picture of an attack and corelate indicators

Everything discussed here so far come together when mapping out an adversary based on threat intel. 