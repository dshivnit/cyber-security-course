24h 7d Operation.

- Find vulnerabilities on a network
	- Outdated systems needing to be patched
		- not necessarily the responsibility of the SOC Team, however, all for the cause!
	- Amongst other vulns
- Detect unauthorised activity
	- Speaks for itself
- Discover policy violations
	- Policies dictate what is allowed and what isn't
	- Speaks for itself
- Detect intrusions
	- Speaks for itself
	- However remember, there are various components that make up a system - ie, web systems, networks (various, multiple devices can be detailed here), server/infrastructure nodes etc
- Support with the incident response
	- the *incident* can be an observation, a policy violation, an intrusion attempt, or something more damaging such as a full on breach
	- The SOC can assist the Incident Response Team in critical/major situations/incidents

Main Data Sources Used:
- Server Logs
	- Always consider the various types of Servers there are in commission 
	- Logs will detail various, almost every action item that happens on a server, a common one would be numerous incorrect logins which would raise flags
	- Grep is your friend ^ _ ^ as is le pipe | (not other kinds of pipe, ye twat)
- DNS Activity
	- Mainly inspecting internal DNS requests
- Firewall Logs
	- Logs here can reveal a mass amount of information in regards to what packs are being passed to and from respective networks
	- Ability to pick up anomalies and relevant patterns
- DHCP Logs
	- In particular new devices that have joined the network (unmanaged devices I'd say)

Tools
- SIEM
	- Security Information and Event Management tool
		- Aggregates data from various sources into one system/interface
		- Ease of use and efficient
	- *more to add here*

Services
- Monitor security posture
	- Primary role of the SOC
	- Monitoring the network and devices for alerts, notifications and responding to them as required
- Vulnerability management
	- Systems, patching, identifying and advising respective Teams that related systems need looking into
- Malware analysis
	- Identifying, analysis malware that has reached the network/system
	- Testing in controlled environments
	- Information gathering on said subject and relaying to a different Team for further analysis
- Intrusion detection
	- IDS (Intrusion Detection System)'s are used mainly
	- Used to detect and log intrusions and suspect packets
	- Describing what caused the alert 
- Reporting
	- As it reads, reporting. 

Proactive Services
- Network Security Monitoring (NSM)
	- As it reads
- Threat Hunting
	- Assume that an intrusion has already taken place and hunt the system to see if they can confirm that suspicion
	- Patterns, etc
- Threat Intelligence
	- Learning about APTs and potential adversaries, their TTPs
	- Developing a threat-informed defense
	- Knowledge is also good. Which is why I'm putting all this stuff together, and sharing - because why not :) (if you're reading, cool (=  ))