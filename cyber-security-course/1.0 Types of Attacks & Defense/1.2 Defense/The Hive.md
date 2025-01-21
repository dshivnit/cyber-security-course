https://tryhackme.com/r/room/thehiveproject
https://strangebee.com/
https://github.com/TheHive-Project/TheHive

- A scalable, open-source and freely available Security Incident Response platform
- Designed to assist security analysts and practitioners working in SOCs, CSIRTs and CERTs to track, investigate and act upon identified security incidents in a swift and collaborative manner

- Security analysts can collaborate on investigations simultaneously, ensuring real-time information pertaining to new or existing cases, tasks, observables and IOCs are available to all team members

- A great companion to MISP
	- https://www.misp-project.org/
	- One can synchronise it with one or multiple MISP instances to start investigations out of MISP events
	- One can also export an investigation's results as a MISP event to help your peers detect and react to attacks you've dealt with

- When used in conjunction with Cortex
	- https://github.com/TheHive-Project/Cortex/
	- Security analysts and researchers can easily analyse tens if not hundred of observables

The Hive
- Collaborate
	- Multiple analysts from one organisation can work together on the same case simultaneously
	- Through its live stream capabilities, everyone can keep an eye on the cases in real time
- Elaborate
	- Investigations correspond to cases
	- The details of each case can be broken down into associated tasks, which can be created from scratch or through a template engine. 
	- Additionally, analysts can record their progress, attach artifacts of evidence and assign tasks effortlessly
- Analyse
- Act
	- A quick triaging process can be supported by allowing analysts to add observables to their case, leveraging tags, flagging IOCs and identifying previously seen observables to feed their threat intelligence

Features:
- Alert management
- Case management
- Multi-tenant environments
- Advanced user management
- Notifications framework
- Metrics and dashboards
- Comprehensive APIs
- MISP integration
- MITRE ATT&CK integration
- Case reporting
- Knowledge base
- Timelines

Features & Integrations
- Case/Task Management
	- Every investigation is supposed to correspond to a case that has been created
	- Each case can be broken down into one or more tasks for added granularity and even be turned into templates for easier management. 
	- Analysts can record their progress, attach pieces of evidence or noteworthy files, add tags and other archives to cases
- Alert Triage
	- Cases can be imported from SIEM alerts, email reports and other security even sources
	- Allows analysts to go through the imported alerts and decide whether or not they are to be escalated into investigations or incident response
- Observable Enrichment with Cortex
	- Cortex is an observable analysis and active responses engine
	- Cortex allows analysts to collect more information from threat indicators by performing correlation analysis and developing patterns from the cases
- Active Response
	- Statistics on cases, tasks, observables, metrics and more can be compiled and distributed on dashboards that can be used to generate useful KPIs within an organisation
- Build-in MISP Integration
	- MISP is a threat intelligence platform for sharing, storing and correlating IOCs of targeted attacks and other threats
	- This integration allows analysts to create cases from MISP events, import IOCs or export their own identified indicators to their MISP communities

- TheHive supports DigitalShadows2TH and ZeroFox2TH - which are free and open-source extensions of alert feeders from DigitalShadows and ZeroFox
	- https://github.com/TheHive-Project/DigitalShadows2TH
	- https://github.com/TheHive-Project/Zerofox2TH
	- https://www.reliaquest.com/security-operations-platform/digital-risk-protection/
	- https://www.zerofox.com/
- These integrations ensure that alerts can be added into TheHive and transformed into new cases using pre-defined incident response templates or by adding to existing cases

Case Descriptions
- Severity
	- Level of impact the incident being investigated has on the environment (low, medium, high, critical)
- TLP
	- Traffic Light Protocol
	- Set of designations to ensure that sensitive information is shared with the appropriate audience
	- The range of colours represents a scale between full disclosure information (WHITE), No Disclosure/Restricted (RED)
		- More can be found about these designations on the CISA website (https://www.cisa.gov/news-events/news/traffic-light-protocol-tlp-definitions-and-usage)
		- RED
			- Not for disclosure
			- Restricted to participants only
		- AMBER + Strict
			- Limited disclosure
			- Restricted to participants' organisation
		- AMBER
			- Limited disclosure
			- Restricted to participants' organisation AND its clients
		- GREEN
			- Limited disclosure
			- Restricted to the community
		- WHITE/CLEAR
			- Disclosure is not limited
- PAP
	- Permissible Actions Protocol
		- Used to indicate what an analyst can do with the information, whether an attacker can detect the current analysis state or defensive actions in place
		- Uses a colour scheme similar to TLP and is part of the MISP Taxonomies (https://www.cisa.gov/news-events/news/traffic-light-protocol-tlp-definitions-and-usage)
			- RED
				- Non-detectable actions only
				- Recipients may NOT use RED information on the network
				- Only passive actions on logs, that are not detectable from the outside
			- AMBER
				- Passive cross check
				- Recipients may use AMBER information for conducting online checks
					- Like using third-party services (VirusTotal) or to set up a monitoring honeypot
			- GREEN
				- Active actions allowed
				- Recipients may use GREEN information to ping the target, block incoming/outgoing traffic from/to the target or specifically configure honeypots to interact with the target
			- CLEAR
				- No restrictions in using this information
			- WHITE
				- No restrictions in using this information
				- 